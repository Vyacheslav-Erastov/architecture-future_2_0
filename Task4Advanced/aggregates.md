# Описание ключевых агрегатов

## 1. Customer Context
### Aggregates:
- **Customer**  
  - Границы: идентификатор клиента, персональные данные (ФИО, дата рождения, контакты), согласия на обработку данных.  
  - Инварианты: уникальность email/телефона, согласия должны быть явно подтверждены.  
  - Ключи: customerId (UUID).  
  - События: CustomerRegistered, CustomerUpdated.

## 2. Medical Context
### Aggregates:
- **Patient**  
  - Границы: идентификатор пациента (совпадает с customerId), медицинская карта (номер), прикреплённый врач, полис ОМС/ДМС.  
  - Инварианты: пациент должен быть зарегистрирован в Customer Context.  
  - Ключи: patientId (UUID).  
  - События: PatientCreated, PatientMoved (смена врача).

- **Appointment**  
  - Границы: время приёма, врач, пациент, статус (запланирован, завершён, отменён).  
  - Инварианты: у врача не может быть двух приёмов одновременно.  
  - Ключи: appointmentId (UUID).  
  - События: AppointmentScheduled, AppointmentCompleted, AppointmentCancelled.

- **Diagnosis**  
  - Границы: код диагноза (МКБ-10), описание, дата постановки, связанный приём.  
  - Инварианты: диагноз может быть поставлен только после завершённого приёма.  
  - Ключи: diagnosisId (UUID).  
  - События: DiagnosisRecorded.

- **ImagingStudy**  
  - Границы: тип исследования (рентген, МРТ и т.д.), дата, статус, ссылки на результаты.  
  - Инварианты: исследование может быть запрошено только для существующего пациента.  
  - Ключи: studyId (UUID).  
  - События: ImagingStudyRequested, ImagingStudyCompleted.

## 3. AI Diagnostics Context
### Aggregates:
- **AIAnalysis**  
  - Границы: идентификатор исследования, модель ИИ, входные данные (изображения/сигналы), результат анализа, статус.  
  - Инварианты: результат должен содержать метрики уверенности.  
  - Ключи: analysisId (UUID).  
  - События: AIAnalysisRequested, AIAnalysisCompleted.

## 4. Fintech Context
### Aggregates:
- **Account**  
  - Границы: номер счёта, владелец (customerId), баланс, валюта, статус.  
  - Инварианты: баланс не может быть отрицательным (для расчётных счетов), только для кредитных допускается овердрафт.  
  - Ключи: accountId (UUID).  
  - События: AccountOpened, AccountClosed, BalanceChanged.

- **Loan**  
  - Границы: сумма, срок, процентная ставка, график платежей, статус заявки.  
  - Инварианты: сумма кредита не превышает лимит клиента.  
  - Ключи: loanId (UUID).  
  - События: LoanApplicationSubmitted, LoanApproved, LoanDisbursed, LoanRepaid.

## 5. Billing Context
### Aggregates:
- **Invoice**  
  - Границы: номер счёта, сумма, услуги (приёмы, исследования), статус оплаты.  
  - Инварианты: сумма должна совпадать с суммой оказанных услуг.  
  - Ключи: invoiceId (UUID).  
  - События: InvoiceCreated, InvoicePaid.

## 6. Inventory Context
### Aggregates:
- **InventoryItem**  
  - Границы: наименование, количество, единица измерения, минимальный запас.  
  - Инварианты: количество не может быть отрицательным.  
  - Ключи: itemId (UUID).  
  - События: InventoryItemUsed, InventoryLow.

## 7. Staff Context
### Aggregates:
- **StaffMember**  
  - Границы: ФИО, должность, график работы, отделение.  
  - Инварианты: у сотрудника может быть только одна основная должность.  
  - Ключи: staffId (UUID).  
  - События: StaffHired, StaffAssigned, StaffLeft.