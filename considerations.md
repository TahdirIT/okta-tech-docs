## Considrations:

1. Main goal: A project called "tahdir", and we want to extract the functionalities from and create another project called "Okta" with advanced tech, codes with better business methodology.
2. Used Tech:
    - Old Project (Tahdir):
        - Laravel 11
        - Livewire 3 
        - Monlith core-embedded architecture  
    - New Project (Okta v1):
        - Laravel 12
        - Livewire 4
        - Monolithic modular architecture (Using Laravel Modular)
    - Feature updated Project (Okta v2):
        - Micro-services architecture
3. 



## Prompt Context
1. I have a project called "tahdir", and we want to extract the functionalities from and create another project called "Okta".
2. Old project: Laravel 11 & Livewire 3 -> New Project: Laravel 12 & Livewire 4.
3. Old project is monolith, and we want to transfer to Modular Services (Each Major Feature under a Module, benefits from Laravel Modular), and after a while (When there are a largening in the service (the infrastructure usage), we will convert the modules to micro-services.
4. There are accounts' types could interact with one or more service, depends on his permissions or the functionality level (ex: manager, teacher, student, account owner, etc...).
5. There are two projects opened in Cursor under one folder:
<root>/okta-tech-docs (for Tech documents)
<root>/v5website (Old Laravel Project)