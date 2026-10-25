# java-template-service

**The golden path for a new Java microservice.** One click gives you a Spring Boot 4 service with
structured logs, tracing, metrics, health checks, clean error responses, enforced formatting, a
Dockerfile, and a CI pipeline that runs the platform's security gate. You write the feature;
the plumbing is already done.

Part of the [Platform Engineering Workshop](https://github.com/draco121/platform-engineering-workshop) (Lab 1).

## Option 1: click "Use this template" (recommended)

1. Click the green **Use this template** button at the top of this page → **Create a new repository**.
2. Name it after your service, for example `coupon-service`. Public or private both work.
3. Open the new repository's **Actions** tab and watch:
   - **bootstrap** fills in this template with your repository's name (`Coupon Service`,
     package `dev.workshop.couponservice`, owner = your GitHub user) and commits the result.
   - **ci** then builds and tests the service, checks formatting, and runs the platform's
     **security gate** against every library the service ships.
4. About three minutes later: a personalised, tested, security-checked service with a green check mark.

### How it works

GitHub template repositories copy files exactly as they are: they can't fill in names.
[Cookiecutter](https://github.com/cookiecutter/cookiecutter) can. This repository combines both:

```
 "Use this template"  →  new repo (a copy of this one)
         ↓  push of the first commit starts .github/workflows/bootstrap.yml
 cookiecutter template/ with the repo's name  →  commit "Bootstrap Coupon Service"
         ↓  bootstrap starts .github/workflows/ci.yml
 build + tests + formatting  →  platform security gate (central, owned by the platform team)  →  ✅
```

The security gate isn't copied into your repo. Your `ci.yml` *calls* the platform team's
[central workflow](https://github.com/draco121/platform-engineering-workshop/blob/main/.github/workflows/platform-gates.yml),
so when the platform changes a rule, every service picks it up on its next run.

## Option 2: the Cookiecutter command line

```bash
pip install cookiecutter
cookiecutter gh:draco121/java-template-service --directory template
```

Answer the questions, then `cd` into the new folder and `mvn spring-boot:run`.

## What's in the template

| Path | What it is |
|---|---|
| `template/cookiecutter.json` | The questions and their defaults |
| `template/hooks/` | Checks your answers before generating; tidies up after |
| `template/{{cookiecutter.service_slug}}/` | The service itself, with `{{ placeholders }}` |
| `.github/workflows/bootstrap.yml` | Turns a fresh copy into your service (runs once) |
| `.github/workflows/ci.yml` | Build, test, formatting, then the central security gate |

## For the platform team: maintaining this template

- Keep this repository marked as a template: **Settings → General → Template repository**.
- `.github/workflows/ci.yml` must stay identical to `template/{{cookiecutter.service_slug}}/.github/workflows/ci.yml`.
- Changes here only reach **new** services. Existing services don't update automatically: that's
  "template drift", one of the open problems discussed in the workshop.
