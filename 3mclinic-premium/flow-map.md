# 3M Clinic Premium — Карта экранов (User Flow)

```mermaid
graph TD
    %% Base Styles
    classDef default fill:#FCFAF6,stroke:#E8DED1,stroke-width:1px,color:#2A2624;
    classDef screen fill:#F4EFE6,stroke:#9C5426,stroke-width:2px,color:#2A2624,font-weight:bold;
    classDef modal fill:#FFFFFF,stroke:#006039,stroke-width:1px,color:#006039,stroke-dasharray: 5 5;
    classDef highlight fill:#006039,stroke:#006039,stroke-width:1px,color:#FFFFFF;

    %% SCREENS
    Home[1. Главный экран<br/>index.html / index-active.html]:::screen
    Services[2. Услуги / Прайс<br/>services.html]:::screen
    Booking[3. Календарь записи<br/>booking.html]:::screen
    Visits[4. Мои визиты<br/>visits.html]:::screen
    Profile[5. Профиль<br/>profile.html]:::screen

    %% MODALS & BOTTOM SHEETS
    ModQR([Шторка: Карта Лояльности QR]):::modal
    ModService([Шторка: Как вас записать?]):::modal
    ModConfirm([Модалка: Визит подтвержден]):::modal
    ModCancel([Модалка: Отменить визит?]):::modal
    ModCall([Модалка: Свяжитесь с клиникой]):::modal
    ModPlan([Шторка: План лечения]):::modal

    %% GLOBAL NAVIGATION (Tabbar)
    Tabbar((Нижнее меню)):::highlight
    Tabbar -->|Главная| Home
    Tabbar -->|Услуги| Services
    Tabbar -->|Визиты| Visits
    Tabbar -->|Профиль| Profile

    %% FLOW: HOME
    Home -->|Клик на QR-код| ModQR
    Home -->|Клик Записаться| Services
    Home -->|Клик Детали визита| Visits
    Home -->|Клик Перенести визит| ModCall

    %% FLOW: SERVICES
    Services -->|Поиск| SearchBar[Строка поиска]
    Services -->|Клик по услуге| ModService
    ModService -->|Ближайшее время| Booking
    ModService -->|Выбрать врача| Booking

    %% FLOW: BOOKING
    Booking -->|Подтвердить запись| SuccessState[Редирект на Главную / Успех]

    %% FLOW: VISITS
    Visits -->|Таб: Предстоящие| VUpcoming[Ожидает / Подтвержден]
    Visits -->|Таб: Прошедшие| VPast[История визитов]

    VUpcoming -->|Подтвердить| ModConfirm
    VUpcoming -->|Отменить| ModCancel
    VUpcoming -->|Перенести| ModCall

    VPast -->|Повторить запись| Booking
    VPast -->|План лечения| ModPlan

    %% FLOW: PROFILE
    Profile -->|Поиск по документам| SearchBar
    Profile -->|Клик на QR-код| ModQR
```
