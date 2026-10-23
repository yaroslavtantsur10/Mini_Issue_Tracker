# 06 — Figma Generation & Correction Report

**Figma:** https://www.figma.com/design/B5nr6SR4YnQztz8cmqTPaa/Untitled?node-id=0-1&t=WWZYHXKmtHtdEB83-1

## Generation (F1)
За відомим перебігом роботи Figma Agent сформував редаговані grayscale desktop frames (1440×900), Auto Layout, локальні компоненти, списки, модальне створення, деталі issue та допоміжні стани. **Точний історичний prompt, дата генерації та повний машинний звіт недоступні; не реконструюються як дослівні.**

## Correction (F2)
- Студент вручну налаштовував зв'язки Prototype: All/Important, ISS-003→Details, Create/Cancel/validation.
- Створено копію `Issue Details — Comment Added`: Comments (2)→Comments (3), додано приклад `Checked and confirmed the fix.` і `Member A · 23 Oct 2026, 14:15 UTC`.
- Кнопку Add Comment з оригінального Details спрямовано на копію — **симуляція успіху**, не фактичне збереження.
- Усунуто помилкові `On drag`/Hover переходи до Supplementary Comment Errors; налаштовано `On click`.
- Користувач повідомив, що після виправлення перехід у Present mode спрацював.

## Що не підтверджено
Повний набір status transitions, права для кожної ролі, серверне збереження, обов'язкові поля на всіх шляхах, безпека та NFR.

**Перевірка:** ручне проходження окремих переходів у Figma Present. **Докази:** скриншоти екранів у `evidence/`; результат натискання Add Comment зафіксовано в журналі тестів.
