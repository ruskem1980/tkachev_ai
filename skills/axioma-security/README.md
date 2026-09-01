# axioma-security

Skill for Claude Code / Агент-скил для Claude Code

Deep security & Russian data-protection (152-ФЗ) website audit — with legal mapping and
rouble-denominated risk pricing.

Глубокий аудит безопасности сайта и соответствия 152-ФЗ — с привязкой к нормам и стоимостной
оценкой риска в рублях.

---

## RU — что это и зачем

`axioma-security` — воспроизводимый порядок бескомпромиссного аудита веб-ресурса. Скил ведёт
исполнителя от разрешения на тест до сдаваемого отчёта и отвечает на три вопроса, каждый — в
рублях:

- **можно ли извлечь данные** — какие поля, каким усилием, какой объём;
- **нарушает ли ресурс закон** — 152-ФЗ, 242-ФЗ, требования Роскомнадзора, с привязкой каждой
  находки к статье и вилке штрафа;
- **сколько это стоит** — ожидаемый ущерб по сценарию и приоритет устранения.

### Зачем нужен

Обычный пентест-отчёт говорит «есть XSS» — но не говорит собственнику, сколько это стоит и какой
закон нарушен. Обычный аудит 152-ФЗ проверяет бумаги — но не проверяет, можно ли реально вытащить
данные. Этот скил соединяет оба слоя: каждая техническая находка переводится в норму и в рубли,
поэтому отчёт понятен и инженеру, и собственнику, и юристу.

### Как работает

Восемь этапов, каждый закрывается артефактом:

| Этап | Содержание |
|---|---|
| 0. Подготовка | Scope, письменное разрешение (ст. 272 УК), карта активов |
| 1. Пассивная разведка | OSINT, DNS, поддомены, subdomain takeover, SPF/DKIM/DMARC, утёкшие данные |
| 2. Транспорт и заголовки | TLS, заголовки безопасности, CORS, cookie |
| 3. Приложение | OWASP: инъекции, десериализация, XSS, IDOR/BFLA, JWT/OAuth, SSRF, API, CVE |
| 4. Персональные данные | Что собирается, где хранится, куда утекает |
| 5. Соответствие 152-ФЗ | Согласия, локализация, cookie, трансграничка, обработчики, модель угроз ФСТЭК/ФСБ |
| 6. Стоимость риска | Множитель вероятности × вилка штрафа + ущерб; CVSS; приоритет P0/P1/P2 |
| 7. Отчёт | Сводка, реестр находок, матрица соответствия, план устранения |

**Стоимость риска** считается детерминированно: множитель вероятности (0,7 / 0,4 / 0,1) ×
середина вилки штрафа + прочий ущерб. Справочник санкций (КоАП ст. 13.11, УК ст. 272.1,
требования 152-ФЗ, ФСТЭК/ФСБ) вынесен в отдельный файл и сверяется на дату отчёта.

### Файлы

- `skills/axioma-security/SKILL.md` — операционный гид (этапы, множители, реестр находок, проверки).
- `skills/axioma-security/references/methodology.md` — полная методология, 17 разделов.
- `skills/axioma-security/references/fines-152fz.md` — справочник санкций и норм.

### Установка

Скопировать каталог `skills/axioma-security/` в `~/.claude/skills/`:

```bash
cp -R skills/axioma-security ~/.claude/skills/
```

Запуск: `/axioma-security` или `Skill(skill="axioma-security")`. Скил также поднимается сам по
триггерам (аудит сайта, пентест, проверка 152-ФЗ, оценка риска утечки ПДн).

### Границы

Активный тест — только по письменному разрешению владельца ресурса (ст. 272 УК РФ). Без
разрешения скил переключается на пассивно-документарный аудит. Правовые суммы актуальны на дату
в справочнике и сверяются с действующей редакцией перед боевым отчётом.

---

## EN — what it is and why

`axioma-security` is a reproducible playbook for an uncompromising website audit. It walks the
operator from test authorization to a deliverable report and answers three questions, each priced
in roubles:

- **can data be extracted** — which fields, at what effort, in what volume;
- **does the site break the law** — Russian data-protection law (152-ФЗ), data-localization law
  (242-ФЗ), regulator (Roskomnadzor) requirements, with every finding mapped to an article and a
  fine range;
- **what does it cost** — expected damage per scenario and remediation priority.

### Why it exists

A normal pentest report says "there is an XSS" but not what it costs the owner or which law it
breaks. A normal 152-ФЗ compliance check reviews paperwork but not whether data can actually be
pulled. This skill fuses both layers: every technical finding is translated into a legal norm and
into money, so the report reads for the engineer, the owner, and the lawyer alike.

### How it works

Eight phases, each closed by an artifact:

| Phase | Content |
|---|---|
| 0. Prep | Scope, written authorization (Criminal Code art. 272), asset map |
| 1. Passive recon | OSINT, DNS, subdomains, subdomain takeover, SPF/DKIM/DMARC, leaked data |
| 2. Transport & headers | TLS, security headers, CORS, cookies |
| 3. Application | OWASP: injections, deserialization, XSS, IDOR/BFLA, JWT/OAuth, SSRF, API, CVEs |
| 4. Personal data | What is collected, where stored, where it leaks |
| 5. 152-ФЗ compliance | Consents, localization, cookies, cross-border transfer, processors, FSTEC/FSB threat model |
| 6. Risk pricing | Likelihood multiplier × fine range + damage; CVSS; priority P0/P1/P2 |
| 7. Report | Executive summary, findings registry, compliance matrix, remediation plan |

**Risk cost** is computed deterministically: likelihood multiplier (0.7 / 0.4 / 0.1) × midpoint of
the fine range + other damage. The sanctions reference (Administrative Code art. 13.11, Criminal
Code art. 272.1, 152-ФЗ / FSTEC / FSB requirements) lives in a separate file and is verified against
the law in force at report date.

### Files

- `skills/axioma-security/SKILL.md` — operational guide (phases, multipliers, findings registry, checks).
- `skills/axioma-security/references/methodology.md` — full methodology, 17 sections.
- `skills/axioma-security/references/fines-152fz.md` — sanctions and norms reference.

### Install

Copy `skills/axioma-security/` into `~/.claude/skills/`:

```bash
cp -R skills/axioma-security ~/.claude/skills/
```

Run with `/axioma-security` or `Skill(skill="axioma-security")`. It also auto-loads on triggers
(website audit, pentest, 152-ФЗ check, PII-leak risk assessment).

### Scope note

Active testing only with written authorization from the resource owner (Criminal Code art. 272).
Without it, the skill switches to a passive, documentary-only audit. Legal amounts are current as of
the date in the reference file and must be re-verified against the law in force before a live report.

---

Legal reference is Russian law as of September 2026; verify amounts before operational use.
Правовой справочник — право РФ на сентябрь 2026; суммы сверять перед боевым применением.
