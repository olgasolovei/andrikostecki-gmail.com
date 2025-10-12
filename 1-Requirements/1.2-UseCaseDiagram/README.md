# Діаграма варіантів використання програмного продукту

```plantuml
@startuml
left to right direction

' Групування акторів по рівнях
rectangle "Рівень адміністрування" {
  actor "Системний\nадміністратор" as Admin
  actor "Керівник IT-\nвідділу" as ITHead
}

rectangle "Рівень аналітики" {
  actor "Аналітик" as Analyst
  actor "Керівник відділу\nзакупівель" as PurchaseHead
  actor "Фінансовий\nдиректор" as FinanceDir
}

rectangle "Рівень операцій" {
  actor "Менеджер з\nзакупівель" as Manager
  actor "Головний\nінженер" as ChiefEng
  actor "Керівник\nпроекту" as ProjectHead
  actor "Фінансовий\nконтролер" as FinanceController
}

' Система та Use Cases
rectangle "Система моніторингу закупівель" {
  package "Адміністрування" {
    usecase "UC001: Керування\nкористувачами системи" as UC1
  }
  
  package "Аналітика" {
    usecase "UC002: Перегляд аналітики\nта звітів" as UC2
  }
  
  package "Закупівлі" {
    usecase "UC003: Пошук та порівняння\nпостачальників" as UC3
    usecase "UC004: Формування заявки\nна закупівлю" as UC4
  }
  
  UC3 --> UC4 : <<include>>
}

' Основні зв'язки - суцільні лінії
Admin --> UC1
Analyst --> UC2
Manager --> UC3
Manager --> UC4

' Додаткові зв'язки - пунктирні лінії
ITHead -[dashed]-> UC1
PurchaseHead -[dashed]-> UC2
FinanceDir -[dashed]-> UC2
ChiefEng -[dashed]-> UC3
ProjectHead -[dashed]-> UC3
ProjectHead -[dashed]-> UC4
FinanceController -[dashed]-> UC4
Admin -[dashed]-> UC4

' Легенда
legend right
  == Легенда ==
  | Суцільна лінія | Основний актор |
  | Пунктирна лінія | Додатковий актор |
  | Include | Обов'язкове включення |
end legend

@enduml
