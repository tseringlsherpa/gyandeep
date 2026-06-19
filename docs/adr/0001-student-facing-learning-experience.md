# ADR 0001: Student-Facing Learning Experience

## Status
Accepted

## Date
2026-06-19

## Context
DeepGyan is a personalized AI learning platform for Nepali high-school students. The current prototype includes a student workflow: upload or select a textbook PDF, view textbook pages, ask questions, receive grounded answers, and optionally generate explanatory animations.

The project is also intended to support randomized controlled trial research with University of Washington researchers and classroom implementation partners such as Teach for Nepal. That research context makes the student-facing experience more than a general chat interface. It must be stable enough for intervention fidelity, observable enough for learning analytics, and constrained enough to avoid contaminating the study with uncontrolled features.

The near-term pilot and RCT planning should prioritize teacher-facing use because teacher adoption, school leadership, infrastructure, and implementation support are expected to determine whether the platform is used at all. Student-facing DeepGyan remains part of the long-term product vision and may become a future treatment arm, but it should not be assumed to be the first intervention surface.

The student interface must work in classroom and home environments where students may have limited time, variable connectivity, shared devices, phone-first access, and mixed literacy in Nepali and English. It should help students learn from assigned materials and continue work away from the screen through writing, paper exercises, prototypes, discussion, or other classroom activities.

## Decision
DeepGyan will maintain a dedicated student-facing learning experience as a long-term learning surface and as a possible future RCT treatment arm.

The student experience will:

- Prioritize textbook-grounded question answering over general-purpose chat.
- Keep the PDF or assigned learning material visible alongside the AI response.
- Support current-page and whole-book context modes when pedagogically appropriate.
- Capture structured learning events for research and product evaluation.
- Avoid exposing research assignment status, treatment labels, or experimental mechanics to students.
- Minimize personally identifying information in product flows and logs.
- Keep optional enrichment features, such as generated animations, traceable to the same source material and student query.
- Be designed for low-bandwidth, low-infrastructure settings and eventual phone-first access where appropriate.
- Encourage learning activities beyond screen time, including paper-based reasoning, classroom discussion, and hands-on work.
- Remain locally grounded in Nepali curriculum, language, culture, geography, and classroom realities.
- Be shaped through research-practice co-design rather than treated as a finished product to be handed to schools.

Student-visible features should be introduced behind configuration or feature flags when they could affect RCT treatment conditions, dosage, or comparability across cohorts.

During the initial teacher-facing pilot, student-facing capabilities may remain available for development and demonstration, but should not be broadly released into study schools unless the research design explicitly includes a student-facing or mixed teacher-plus-student treatment condition.

## Rationale
For an RCT, any student-facing system can become part of the intervention. The experience needs to be consistent across participating classrooms and students so observed outcomes can be interpreted with confidence.

Grounding answers in uploaded or assigned textbooks supports curriculum alignment and reduces the risk of the assistant becoming an unrelated tutoring product. Keeping the source material visible also helps students connect AI responses back to classroom content.

Structured event capture allows researchers and the product team to distinguish between access, engagement, usage intensity, and learning activity. That distinction matters for implementation fidelity and later analysis.

Student-facing DeepGyan should eventually support learners who are outside ideal school settings, including students with irregular school attendance, limited access to teachers, or stronger access to phones than computer labs. That long-term promise should not override the near-term need to learn whether teachers and schools can adopt the platform.

## Consequences
Positive consequences:

- The main student workflow remains simple and classroom-oriented.
- Product analytics can support RCT fidelity checks without adding separate research instrumentation later.
- New student features have a clear review standard: they must preserve source grounding and study comparability.
- The product can later test teacher-only, student-only, and mixed teacher-plus-student interventions without redesigning the student surface from scratch.

Tradeoffs:

- Some useful exploratory AI features may need to wait until after study design review.
- Feature flags and event schemas add implementation overhead.
- The student UI must avoid research language even when the backend stores research-relevant metadata.
- Student-facing work may progress more slowly while teacher adoption and pilot fidelity are validated.

## Implementation Notes
The student-facing surface should continue to use the existing dashboard PDF viewer, chat workflow, OCR, embeddings, and learning event storage as its foundation.

Future implementation work should add or preserve:

- Stable event names for uploads, page views, prompts, responses, retrieval mode changes, animation requests, and feedback.
- A student or participant identifier strategy that can support research linkage without exposing unnecessary PII.
- Feature flags for intervention variants.
- Audit-friendly metadata in `learning_events.metadata` for source book, page range, retrieval mode, model/provider, and feature state.
- Clear separation between student-facing state and teacher/researcher-facing reporting.
- Accessibility for low-literacy and multilingual contexts, with careful evaluation before adding voice, avatar, or other high-salience features.
- Mobile-friendly interaction patterns for later home and out-of-school use.
- Guardrails and evaluation records for factuality, grounding, safety, cultural alignment, and age-appropriate responses.
- Offline or degraded-connectivity design options where school infrastructure makes always-online use unrealistic.

## Non-Goals
This ADR does not define the final research protocol, consent process, assessment instruments, statistical analysis plan, or timing for student-facing deployment in study schools. It only records product and architecture decisions needed to keep the student-facing experience suitable for future RCT use.
