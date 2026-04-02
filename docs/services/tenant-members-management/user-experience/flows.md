# التدفقات (Flows) — Tenant Members Management

## 1) إضافة طالب يدوياً (Manual add student)

```mermaid
flowchart TD
  OpenModal[OpenAddStudentModal] --> EnterNationalId[EnterNationalId]
  EnterNationalId --> CheckExisting[CheckExistingUserStudent]
  CheckExisting -->|AlreadyInTenant| ErrorInTenant[ShowAlreadyLinkedError]
  CheckExisting -->|InOtherTenant| ErrorOtherTenant[ShowOtherTenantError]
  CheckExisting -->|OK| FillData[FillStudentData]
  FillData --> SelectStage[SelectStage]
  SelectStage --> SelectSection[SelectSection]
  SelectSection --> Save[Save]
  Save --> Success[SuccessAndRefresh]
```

نقاط إلزامية:

- لا يمكن حفظ الطالب بدون `stage` و`section`.

## 2) تعديل بيانات الطالب ونقله لفصل آخر

```mermaid
flowchart TD
  OpenEdit[OpenStudentDataModal] --> EditFields[EditFields]
  EditFields --> ChangeStage[ChangeStageOptional]
  ChangeStage --> ResetSection[ResetSection]
  ResetSection --> SelectSection[SelectNewSection]
  SelectSection --> Save[Save]
  Save --> UpdateHistory[ReleaseOldLinkAndAttachNew]
  UpdateHistory --> Success[Success]
```

## 3) ربط ولي أمر بالطالب

```mermaid
flowchart TD
  OpenLink[OpenLinkGuardianModal] --> EnterGuardianId[EnterGuardianNationalId]
  EnterGuardianId --> CheckGuardian[CheckUserGuardian]
  CheckGuardian -->|NotFound| CreateGuardian[CreateGuardianUserAndGuardian]
  CheckGuardian -->|Found| Link[CreateGuardianStudentLink]
  CreateGuardian --> Link
  Link --> Success[Success]
```

## 4) استيراد طلاب عبر ملف

```mermaid
flowchart TD
  Upload[UploadFile] --> Parse[ParseUsingSchema]
  Parse --> Preview[PreviewRows]
  Preview --> Validate[ValidateRows]
  Validate -->|Errors| Fix[UserFixesRowsOrRemoves]
  Validate -->|OK| Execute[ExecuteImport]
  Execute --> Upsert[UpsertUsersAndStudents]
  Upsert --> LinkTenant[AttachToTenant]
  LinkTenant --> LinkSection[AttachToSectionsAndSetActive]
  LinkSection --> Jobs[DispatchPostJobs]
  Jobs --> Done[Done]
```

