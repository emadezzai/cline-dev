# Tasks: Arabic Chat Localization

**Input**: Design documents from `/specs/arabic-chat/`
**Prerequisites**: plan.md ✓, spec.md ✓

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to

## Phase 1: Infrastructure Setup

**Purpose**: إنشاء البنية التحتية لنظام الترجمة

- [ ] T001 [P] [US1] Create `webview-ui/src/locales/ar-sa/` directory structure
- [ ] T002 [P] [US1] Create `webview-ui/src/locales/ar-sa/chat.json` with initial translations
- [ ] T003 [P] [US1] Create `webview-ui/src/utils/localization.ts` with localization utilities
- [ ] T004 [P] [US1] Create `webview-ui/src/hooks/useLanguage.ts` hook for language management
- [ ] T005 [P] [US1] Create `webview-ui/src/context/LanguageContext.tsx` React context

**Checkpoint**: Infrastructure ready - can proceed to UI changes

---

## Phase 2: RTL Support

**Purpose**: دعم الاتجاه من اليمين لليسار (RTL) - Story 2

**⚠️ CRITICAL**: RTL must work before any Arabic UI can be tested

### Implementation for RTL Support

- [ ] T010 [P] [US2] Add RTL CSS utilities in Tailwind config (if needed)
- [ ] T011 [P] [US2] Update ChatInput.tsx to support RTL input
- [ ] T012 [P] [US2] Update ChatMessages.tsx to support RTL layout
- [ ] T013 [P] [US2] Update ChatBubble.tsx for RTL message alignment
- [ ] T014 [US2] Add dir="rtl" attribute to chat container when Arabic selected
- [ ] T015 [US2] Handle mixed LTR/RTL text in input field

**Checkpoint**: RTL support working - can now test Arabic UI

---

## Phase 3: User Story 1 - Arabic Chat Interface

**Goal**: جميع عناصر واجهة الدردشة تظهر بالعربية

### Implementation for Arabic Interface

- [ ] T020 [US1] Translate static UI elements in chat components (buttons, labels, headers)
- [ ] T021 [US1] Update ChatToolbar.tsx with Arabic labels
- [ ] T022 [US1] Add Arabic translations for system messages (loading, empty states, etc.)
- [ ] T023 [US1] Translate tooltips and placeholders in chat components

**Checkpoint**: User Story 1 complete - basic Arabic UI working

---

## Phase 4: User Story 2 - Arabic Input

**Goal**: دعم إدخال النص العربي بشكل صحيح

### Implementation for Arabic Input

- [ ] T030 [US2] Ensure proper font rendering for Arabic in input
- [ ] T031 [US2] Handle Arabic keyboard events correctly
- [ ] T032 [US2] Test copy/paste of Arabic text in input field
- [ ] T033 [US2] Verify auto-direction detection works correctly

**Checkpoint**: User Story 2 complete - Arabic input working

---

## Phase 5: User Story 3 - Arabic Date/Time

**Goal**: عرض التاريخ والوقت بالعربية

### Implementation for Arabic Date/Time

- [ ] T040 [P] [US3] Create `webview-ui/src/utils/dateUtils.ts` for Arabic date formatting
- [ ] T041 [P] [US3] Update message timestamps to use Arabic format when Arabic selected
- [ ] T042 [P] [US3] Add relative time strings (الآن, منذ X دقائق, etc.) in ar-sa/chat.json
- [ ] T043 [US3] Update all time display locations in chat components

**Checkpoint**: User Story 3 complete - Date/Time in Arabic

---

## Phase 6: User Story 4 - Arabic Error Messages

**Goal**: رسائل الخطأ والتحذيرات بالعربية

### Implementation for Arabic Errors

- [ ] T050 [P] [US4] Add Arabic error messages to `ar-sa/chat.json`
- [ ] T051 [P] [US4] Update error handling components to use translated messages
- [ ] T052 [US4] Add Arabic confirmation dialog messages
- [ ] T053 [US4] Test all error scenarios with Arabic locale

**Checkpoint**: User Story 4 complete - Errors in Arabic

---

## Phase 7: User Story 5 - Arabic Tool Names (Optional)

**Goal**: أسماء الأدوات بالعربية

### Implementation for Arabic Tools

- [ ] T060 [P] [US5] Add Arabic tool names and descriptions to `ar-sa/chat.json`
- [ ] T061 [P] [US5] Update tool display components to use translated names
- [ ] T062 [US5] Verify tool descriptions render correctly in Arabic

**Checkpoint**: User Story 5 complete - Tools in Arabic (if implemented)

---

## Phase 8: Testing & Polish

**Purpose**: Testing and cross-cutting concerns

### Testing

- [ ] T070 [P] Create `webview-ui/tests/chat/ChatLocalization.test.tsx`
- [ ] T071 [P] Create `webview-ui/tests/chat/RTLSupport.test.tsx`
- [ ] T072 [P] Test all User Stories independently
- [ ] T073 Test language switching during active conversation
- [ ] T074 Test mixed Arabic/English text scenarios

### Polish

- [ ] T080 [P] Review Arabic translations for natural language
- [ ] T081 [P] Verify all Arabic text fits within UI components
- [ ] T082 [P] Test with different Arabic fonts if needed
- [ ] T083 Run existing tests to ensure no regressions

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 1 (Infrastructure)**: No dependencies
- **Phase 2 (RTL)**: Depends on Phase 1
- **Phase 3-7 (User Stories)**: All depend on Phase 2
- **Phase 8 (Testing)**: Depends on all previous phases

### Parallel Opportunities

- T001-T005 can run in parallel
- T010-T015 can run in parallel
- T030-T033 can run in parallel
- T040-T043 can run in parallel
- T050-T053 can run in parallel
- T070-T074 can run in parallel
- T080-T083 can run in parallel

---

## Notes

- [P] tasks = parallelizable (different files)
- Start with Phase 1 to establish infrastructure
- RTL support (Phase 2) is critical before UI testing
- User Stories 1 & 2 are the MVP (Priority P1)
- User Stories 3, 4, 5 are enhancements (Priority P2/P3)
