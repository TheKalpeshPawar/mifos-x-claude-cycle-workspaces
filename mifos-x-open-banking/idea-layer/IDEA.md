# mifos-x-open-banking — Product Idea

> Auto-generated from `idea-plan.yaml` §vision + §personas + §branding on 2026-05-20.
> Edit `idea-plan.yaml` and run `/idea sync` to regenerate.

## Elevator Pitch

**TaskMinder** is a cross-platform task management application showcasing production-ready KMP architecture — rich features for task creation, calendar-based filtering, priority levels, and completion tracking across Android, iOS, Desktop, and Web.

## Problem

Developers evaluating Kotlin Multiplatform need a realistic reference implementation showing layered architecture, MVI state management, Material 3 design, and multi-platform CI/CD — not just a hello-world.

## Target Users

Developers learning KMP patterns; teams evaluating multiplatform frameworks; end users seeking a lightweight cross-device task manager.

> ⚠️ **Identity disambiguation**: The repo README markets this as "KMP Multi-Module Project Generator" but the actual source is a working TaskMinder task-management app. Treat it as a working app that demonstrates template patterns — not a template skeleton.

---

## Personas

### 👨‍💻 Alex — Developer

A developer evaluating KMP for their next cross-platform project. Seeks reference implementations showing best practices in architecture, testing, and deployment.

**Needs:**
- Clean module structure
- Example ViewModels and Screens
- CI/CD workflow templates
- Design system patterns

### 📝 Maya — End User

A productivity-focused user who wants to manage daily tasks with priority levels and due-date reminders across devices.

**Needs:**
- Quick task entry
- Calendar-based filtering
- Priority organization
- Cross-device sync capability

### 🚀 Rajesh — DevOps / QA

A release engineer or QA lead automating builds and deployments across multiple platforms.

**Needs:**
- Automated build pipelines
- Multi-platform testing
- Release versioning strategy
- Keystore / signing management

---

## Brand

| Token | Value |
|---|---|
| **App name** | TaskMinder |
| **Primary color** | <span style="display:inline-block;width:14px;height:14px;background:#1800B1;border-radius:3px;vertical-align:middle;margin-right:4px;"></span> `#1800B1` (deep purple) |
| **Accent** | `#575899` |
| **Secondary** | `#5C0068` |
| **Design system** | Material Design 3 (light + dark) |
| **Background (light)** | `#FCF8FF` |
| **Background (dark)** | `#13131B` |
| **Logo** | External (referenced in README) |

---

## At a glance

| | |
|---|---|
| **Domain** | task-management / personal-productivity |
| **Platforms** | Android · iOS · Desktop · Web |
| **Tech stack** | Kotlin 2.1.20 · Compose Multiplatform 1.8.2 · Koin · Ktor/Ktorfit · Room KMP · MVI |
| **Backend** | Firebase (Crashlytics + Performance) — observability only |
| **License** | MPL-2.0 |
| **Repo** | [openMF/mifos-x-open-banking](https://github.com/openMF/mifos-x-open-banking) |
