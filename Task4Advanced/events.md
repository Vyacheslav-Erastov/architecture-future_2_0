# Каталог доменных событий

| Название события         | Контекст-источник | Семантика                                    | Минимальный контракт (ключевые поля)          |
| ------------------------ | ----------------- | -------------------------------------------- | --------------------------------------------- |
| CustomerRegistered       | Customer          | Зарегистрирован новый клиент                 | customerId, name, email, phone                |
| CustomerUpdated          | Customer          | Изменены данные клиента                      | customerId, changedFields                     |
| PatientCreated           | Medical           | Создан пациент на основе клиента             | patientId, customerId, policyNumber           |
| AppointmentScheduled     | Medical           | Запланирован приём к врачу                   | appointmentId, patientId, doctorId, time      |
| AppointmentCompleted     | Medical           | Приём завершён                               | appointmentId, outcome                        |
| DiagnosisRecorded        | Medical           | Поставлен диагноз                            | diagnosisId, patientId, code, description     |
| PrescriptionIssued       | Medical           | Выписано лекарство                           | prescriptionId, patientId, medication, dosage |
| ImagingStudyRequested    | Medical           | Запрошено исследование (МРТ, рентген и т.д.) | studyId, patientId, type, requestedAt         |
| ImagingStudyCompleted    | Medical           | Исследование выполнено, результаты готовы    | studyId, resultsUri                           |
| AIAnalysisRequested      | AI Diagnostics    | Отправлено на анализ ИИ                      | analysisId, studyId, modelVersion             |
| AIAnalysisCompleted      | AI Diagnostics    | Получен результат анализа                    | analysisId, result, confidence                |
| InventoryItemUsed        | Inventory         | Использован расходный материал               | itemId, quantity, appointmentId (опц.)        |
| InventoryLow             | Inventory         | Запас материала ниже порога                  | itemId, currentQuantity, threshold            |
| StaffAssigned            | Staff             | Назначен сотрудник на приём/смену            | staffId, appointmentId (или shiftId)          |
| AccountOpened            | Fintech           | Открыт банковский счёт                       | accountId, customerId, currency               |
| LoanApplicationSubmitted | Fintech           | Подана заявка на кредит                      | loanId, customerId, amount, term              |
| LoanApproved             | Fintech           | Кредит одобрен                               | loanId, approvedAmount, rate                  |
| LoanDisbursed            | Fintech           | Средства по кредиту выданы                   | loanId, disbursedAmount, date                 |
| TransactionPosted        | Fintech           | Проведена транзакция по счёту                | transactionId, accountId, amount, type        |
| InvoiceCreated           | Billing           | Выставлен счёт за услуги                     | invoiceId, patientId, amount, items           |
| PaymentReceived          | Billing           | Получена оплата по счёту                     | invoiceId, amount, paymentMethod              |