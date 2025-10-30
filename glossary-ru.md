# Шпаргалка по терминам и аббревиатурам

Документ пополняется по мере проработки архитектуры и слайдов. Короткие определения и зачем это нужно.

## Edge & Delivery
- **CDN (Content Delivery Network)** — распределённая сеть кэширующих узлов для быстрой отдачи статики и медиа с минимальной задержкой.
- **WAF (Web Application Firewall)** — фильтрация и защита HTTP (HyperText Transfer Protocol)‑трафика на периметре (OWASP — Open Web Application Security Project, rate limiting, IP — Internet Protocol блокировки).
- **Edge** — узлы «на краю» сети (PoP — Point of Presence), близко к пользователю; снижают latency и разгружают бэкенд.
- **TLS (Transport Layer Security)** — шифрование трафика «на проводе» (in‑transit). Совместно с шифрованием «на диске» (at‑rest) закрывает основу безопасности.
- **Rate limiting / Throttling** — ограничение частоты запросов для защиты и справедливого распределения ресурсов.
- **TTFB (Time To First Byte)** — время до первого байта ответа; критично для UX. Снижается edge‑кэшированием и оптимизацией сети. См. также: [Caching strategies](#performance--delivery-patterns).

## Access Layer
- **API Gateway (Application Programming Interface)** — единая точка входа, маршрутизация, авторизация, квоты, кэширование, канареечные релизы.
- **BFF (Backend For Frontend)** — бэкенд‑прослойка, адаптирующая API под конкретный клиент (Web/Mobile), минимизирует чаты‑запросы.
- **GraphQL (Graph Query Language)** — схема+резолверы для выборки ровно необходимых полей; альтернатива REST (Representational State Transfer).

## Identity & Privacy
- **OAuth 2.0 (Authorization Framework) / OIDC (OpenID Connect)** — стандарты авторизации и федеративной аутентификации, токены доступа/обновления/ID‑токены.
- **RBAC (Role‑Based Access Control) / ABAC (Attribute‑Based Access Control)** — контроль доступа по ролям/атрибутам.
- **Consent** — согласия пользователя на обработку/коммуникации; хранение и аудит изменений согласий.
- **PII (Personally Identifiable Information)** — персональные данные, требующие особой защиты.
- **DSAR (Data Subject Access Request)** — запрос субъекта данных (экспорт/удаление в срок по закону).
- **Tokenization** — замена чувствительных полей токенами; хранение оригиналов в защищённом хранилище.

## Data Integration & Eventing
- **MLS (Multiple Listing Service)** — источники объявлений о недвижимости; десятки форматов и частот обновлений.
- **RESO (Real Estate Standards Organization)** — спецификации (например, RESO Data Dictionary) для унификации MLS‑данных.
- **Event Bus (Kafka / PubSub — Publish‑Subscribe)** — асинхронная шина событий для интеграций и реактивной обработки.
- **Topic / Partition** — логическая/физическая сегментация потока сообщений; масштабирование потребления.
- **Schema Registry** — реестр схем (Avro / JSON — JavaScript Object Notation / Protobuf — Protocol Buffers) для эволюции контрактов данных.
- **CDC (Change Data Capture)** — фиксация изменений в БД как поток событий.
- **Outbox pattern** — надёжная публикация событий из транзакций приложения, избежание «двойной записи».

## Processing & Orchestration
- **Streaming / Batch** — потоковая/пакетная обработка; выбор по требуемой свежести и стоимости.
- **Idempotency (идемпотентность)** — повторная обработка без побочных эффектов.
- **Deduplication (дедупликация)** — устранение дублей (по ключам/эвристикам/окнам времени).
- **Backpressure** — управление скоростью при перегрузке потребителей.
- **Delivery semantics** — at‑least‑once / at‑most‑once / exactly‑once гарантии доставки/обработки.

## Storage & Indexes
- **OLTP (OnLine Transaction Processing)** — транзакционное хранилище для пользовательских операций.
- **Search Index (Elasticsearch / OpenSearch)** — полнотекст и гео‑поиск, агрегации, ранжирование.
- **Data Lake** — «сырое» хранилище больших данных (объектное), формат колоночный, дешёвое длительное хранение.
- **DWH (Data Warehouse)** — витрины и аналитика (Business Intelligence — BI), стабильные схемы, SLA (Service Level Agreement) на отчёты.
- **Object Storage** — хранение медиа/файлов; дешёвое и масштабируемое (S3 — Simple Storage Service / GCS — Google Cloud Storage / Azure Blob Storage).
- **Cache (Redis/Edge/App)** — ускорение чтения; политики инвалидации (TTL — Time‑To‑Live, событие, версия).
- **CQRS (Command Query Responsibility Segregation)** — разделение моделей записи и чтения для производительности/масштабирования.
- **Materialized View (MV)** — предвычисленная таблица/представление для быстрых чтений под сценарии; обновляется инкрементально/по расписанию. Компромисс: свежесть vs стоимость. См. также: [CQRS](#storage--indexes).
- **Read replica** — реплика БД только для чтения; разгружает мастер и снижает латентность чтений. Возможна eventual consistency.
- **Sharding / Shard promotion** — горизонтальное разбиение данных на шарды и перевод реплики в лидер при сбоях.
- **HTAP (Hybrid Transactional/Analytical Processing)** — объединение OLTP и аналитики в одном сторе. Сложно держать SLO разных нагрузок; мы предпочли CQRS + Lake/DWH.
- **LSM‑tree (Log‑Structured Merge)** — класс структур хранения, оптимизированных на запись (часто в KV/поиске); важен для индексов и потоков.

## ML & AVM
- **ML (Machine Learning)** — машинное обучение; модели и инференс.
- **AVM (Automated Valuation Model)** — автоматическая оценка стоимости объекта недвижимости.
- **Feature Store** — централизованное управление фичами: вычисление, версионирование, онлайн/оффлайн доступ.
- **Model Registry** — хранение артефактов моделей, версий, метрик и деплоев.
- **Online serving / Offline training** — онлайн‑инференс с низкой задержкой / оффлайн‑обучение по историческим данным.
- **Retraining / Drift** — переобучение при дрейфе данных/модели для поддержания качества.
- **Explainability / Interpretability** — объяснимость/интерпретируемость моделей и факторов, прозрачные решения.
- **Fairness** — недискриминационные практики в ML. См. также: [Compliance & Governance](#compliance--governance).

## Observability & SRE
- **SRE (Site Reliability Engineering)** — инженерные практики надёжности и эксплуатации.
- **SLI (Service Level Indicator) / SLO (Service Level Objective) / SLA (Service Level Agreement)** — метрика уровня сервиса / целевой уровень / контракт с пользователем.
- **p95 / p99** — квантиль задержки; хвостовые задержки критичны для UX (User Experience).
- **Tracing / Logging / Metrics** — трассировки, логи, метрики для диагностики и алертинга.
- **Circuit Breaker** — предохранитель при деградациях, предотвращает каскадные отказы.
- **Canary Release / Blue‑Green** — постепенное/параллельное выкатывание для снижения риска.
- **RTO / RPO** — Recovery Time / Point Objectives: целевое время восстановления и допускаемая потеря данных.
- **Failover** — автоматическое переключение на резерв (реплика/зона/регион) при сбое.
- **Multi‑AZ / Multi‑region** — развёртывание в нескольких зонах/регионах для отказоустойчивости и ближнего чтения.
## Architecture & Delivery
- **Build vs Buy** — выбор: строить самим или использовать managed/SaaS. Критерии: SLA/операционные риски, дифференциация, стоимость/lock‑in.
- **Managed service** — управляемый провайдером сервис (обновления/патчи/HA). Ускоряет delivery, снижает оперриски.
- **Managed‑first** — стратегия приоритета managed сервисов, а «своё» — там, где дифференцируемся.
- **Lock‑in** — зависимость от вендора; смягчается абстракциями и гибридом.
- **Modular Monolith** — модульный монолит с явными границами; упрощает старт и миграцию к микро‑сервисам.
- **Strangler Fig pattern** — поэтапное выделение модулей монолита в сервисы без «большого взрыва».
- **Contract testing (Pact)** — consumer‑driven контракты для API; проверяет совместимость изменений между сервисами/клиентами.


## Geo & Media
- **Geospatial index** — индексы для гео‑запросов (геохэш/shape‑индексы), фильтры по радиусу/полигону.
- **Tiling / Tiles** — нарезка картинок/данных по тайлам для быстрой отрисовки на карте.
- **Clustering** — агрегация точек (кластеризация) для отображения 1000+ пинов.
- **Geocoding / Reverse geocoding** — адрес ↔ координаты.
- **3D / Virtual Tours** — 3D‑модели объектов для интерактивного просмотра (WebGL/360°).
- **AR (Augmented Reality)** — дополненная реальность для визуализации обстановки/мебели в пространстве.
- **Floor plan** — план этажа/планировка; один из критичных медиа‑типов для карточки объекта.
- **Drone footage** — аэросъёмка с дрона; показывает окружение и участок сверху.
- **Walkability score** — оценка пешеходной доступности района (школы/магазины/транспорт).
- **DOM (Days On Market)** — количество дней, что объект на рынке; показатель ликвидности и аналитика в витринах.

## Compliance & Governance
- **CCPA** — закон Калифорнии о приватности, права пользователей и обязанности провайдеров.
- **TILA‑RESPA** — требования к раскрытию информации и честным кредитным практикам в финсервисах.
- **Fair lending / Anti‑discrimination** — недискриминационные практики; контроль bias моделей/правил.
- **Retention / Legal hold** — сроки хранения/заморозка данных для соответствия требованиям.

## Performance & Delivery Patterns
- **Caching strategies** — cache‑aside / write‑through / write‑back; выбор по консистентности и цене.
- **Pagination / Windowing** — постраничная выборка и оконные операции для потоков/аналитики.
- **Async / Retry / Dead‑letter** — асинхронная обработка с повторами и парковкой «ядовитых» сообщений.
- **DLQ (Dead Letter Queue)** — очередь «ядовитых» сообщений для ручной/отложенной обработки.
- **Exponential backoff (with jitter)** — увеличивающиеся интервалы повтора с рандомизацией, чтобы избежать штормов.
- **Hit‑rate (cache)** — доля попаданий в кэш; ключевой драйвер стоимости и p95. См. также: [Caching strategies](#performance--delivery-patterns).
- **Graceful degradation** — контролируемое упрощение функциональности при пиках/сбоях (меньше пинов, статические тайлы, частичные ответы).
