# Adding a New Block

A block is three things:

1. A PHP class extending `App\LandingBuilder\Contracts\Block`
2. A renderer Blade partial — used on both the editor canvas and the public page
3. An editor Blade partial — used in the inspector sidebar

## 1. The class

```php
namespace App\LandingBuilder\Blocks;

use App\LandingBuilder\Contracts\Block;

class PricingBlock extends Block
{
    public function type(): string           { return 'pricing'; }
    public function category(): string       { return self::CATEGORY_CONVERSION; }
    public function icon(): string           { return 'tag'; }
    public function rendererView(): string   { return 'landing-builder::blocks.pricing.renderer'; }
    public function editorView(): string     { return 'landing-builder::blocks.pricing.editor'; }
    public function labels(): array
    {
        return ['ar' => 'الأسعار', 'en' => 'Pricing'];
    }

    public function defaultContent(string $locale): array
    {
        return $locale === 'en'
            ? ['title' => 'Pricing', 'tiers' => []]
            : ['title' => 'الأسعار', 'tiers' => []];
    }

    // Override validate() if you need structural validation beyond defaults.
    public function validate(array $content, string $locale): array
    {
        $defaults = $this->defaultContent($locale);
        // ...sanitize each tier, drop unknown keys...
        return [
            'title' => (string) ($content['title'] ?? $defaults['title']),
            'tiers' => /* sanitized list */,
        ];
    }
}
```

## 2. Register it

In `LandingBuilderServiceProvider::register()`, add to the main block list or
include it in `discoverMvpBlocks()` (the optional list that loads via
`class_exists`).

## 3. Renderer

`resources/views/landing-builder/blocks/pricing/renderer.blade.php`

```blade
@php
    $pt = (int) data_get($settings, 'padding.top', 64);
    $pb = (int) data_get($settings, 'padding.bottom', 64);
@endphp

<section class="landing-block landing-pricing"
         style="padding-top: {{ $pt }}px; padding-bottom: {{ $pb }}px;">
    <div class="mx-auto max-w-6xl px-6">
        <h2>{{ data_get($content, 'title') }}</h2>
        {{-- ...render tiers... --}}
    </div>
</section>
```

Available Blade variables:

| Var | Shape |
|-----|-------|
| `$block`    | full block record incl. content for all locales |
| `$content`  | `$block['content'][$locale]` already picked |
| `$settings` | `$block['settings']` |
| `$locale`   | `"ar"` / `"en"` |
| `$dir`      | `"rtl"` / `"ltr"` |
| `$theme`    | page-level theme tokens |

## 4. Editor

`resources/views/landing-builder/blocks/pricing/editor.blade.php`

```blade
@php $prefix = "blocks.{$index}.content.{$locale}"; @endphp

<div class="space-y-3">
    <input type="text"
           wire:model.live.debounce.400ms="{{ $prefix }}.title"
           class="w-full px-3 py-2 text-sm rounded-lg border border-slate-300">
</div>
```

Available variables:

| Var | Meaning |
|-----|---------|
| `$block`  | the block record |
| `$index`  | its position inside `$blocks` |
| `$locale` | currently-selected editor locale |

All writes happen through `wire:model` targeting paths inside the Livewire
`Editor` component's state (`blocks.{i}.content.{locale}.<field>`). Server-
side sanitisation happens via `BlockRegistry::sanitize()` on every save, so
malformed paths are dropped rather than persisted.

## 5. Superadmin-only blocks

For Custom HTML / Custom Script / Embed-style blocks that shouldn't be
available to tenant admins, override `superAdminOnly()`:

```php
public function superAdminOnly(): bool { return true; }
```

The editor's sidebar uses `App\Livewire\TenantLanding\Editor::canUseAdvanced`
to filter; regular tenants will never see the block thumb.
Additionally the editor refuses to `addBlock()` for superadmin-only types
unless `canUseAdvanced` is true — so you can't force-insert by URL-hacking
the payload.

## 6. Tests

See `tests/Unit/LandingBuilder/BlockRegistryTest.php` for a template.
Your new block automatically participates in the sanitize / fallback
pipeline; the only block-specific test you usually need is to verify
`validate()` drops unknown keys and sanitises per-locale correctly.
