# 🤖 Битрикс24 + 1С: автоматическая обработка заявок (LLM + n8n)

**Название:** `bitrix24-1c-ai-order-processor`

**Стек:** n8n, OpenAI GPT, REST API, Webhook, Битрикс24 REST API, 1С HTTP-сервис

**Лицензия:** MIT

---

## 📌 О проекте

Автоматическая обработка входящих заявок: классификация через LLM, генерация коммерческого предложения, создание сделки в Битрикс24 и подготовка данных для 1С.

**Архитектура:**

**Что умеет:**
- ✅ Принимает заявку через Webhook
- ✅ Классифицирует тип обращения (заказ / вопрос / жалоба) через LLM
- ✅ Генерирует коммерческое предложение
- ✅ Может создавать сделку в Битрикс24 (замена имитации)
- ✅ Может запрашивать цены и остатки из 1С (замена имитации)
- ✅ Возвращает результат клиенту

---

## 🚀 Быстрый старт (тестирование без CRM)

### 1. Импорт workflow

Скачай `workflow.json` и импортируй в n8n.

### 2. Настрой Webhook

- **Method:** `POST`
- **Path:** `order-request`

**Пример ответа:**
success   : True
message   : Заявка обработана
client    : OOO Romashka
offer     : КОММЕРЧЕСКОЕ ПРЕДЛОЖЕНИЕ...

### 3. Тестовый запрос (PowerShell)

```powershell
$r = Invoke-RestMethod -Uri "https://ваш-домен.amvera.io/webhook-test/order-request" -Method POST -ContentType "application/json" -Body '{"client": "OOO Romashka", "contact": "info@romashka.ru", "message": "Nuzhno 10 noutbukov"}'
$r | Format-List
