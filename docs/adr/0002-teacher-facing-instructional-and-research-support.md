# ADR 0002: Teacher-Facing Instructional and Research Support

## Status
Accepted

## Date
2026-06-19

## Context
DeepGyan needs a student-facing intervention surface and a teacher-facing support surface. Teachers need practical visibility into classroom use: which books are assigned, whether students can access the tool, where students are getting stuck, and whether AI-generated help is aligned with instruction.

Because the project is intended to support RCT research with University of Washington researchers and classroom implementation partners such as Teach for Nepal, the teacher-facing surface also has research implications. Teacher tools can influence implementation fidelity, student encouragement, classroom behavior, and treatment-control separation. A teacher dashboard therefore cannot be treated as a neutral admin add-on.

The near-term pilot should start with teacher-facing use: lesson planning, classroom activity brainstorming, adaptation of textbook content, and teacher enablement. This reflects practical constraints in many Nepali public schools: limited working computer labs, locked or unused devices, inconsistent electricity or connectivity, low computer usage among teachers, and the importance of school leadership support.

The teacher-facing experience must support instruction and implementation monitoring while avoiding premature exposure of outcome comparisons or research labels that could bias classroom behavior during the study. It must also make adoption itself measurable, because the core research and implementation question is not only whether DeepGyan can generate good content, but whether teachers will actually learn, trust, and use it.

## Decision
DeepGyan will define a separate teacher-facing product surface as the first pilot-ready intervention surface for classroom management, lesson planning, instructional visibility, and RCT implementation support.

The teacher-facing experience will:

- Be role-separated from the student learning interface.
- Support lesson planning, classroom activity design, textbook adaptation, and differentiated support based on student profiles and local context.
- Show classroom, book, and usage information needed for instruction and implementation support.
- Prefer aggregate and classroom-level views by default, with student-level drilldowns only when needed for legitimate instructional support.
- Track intervention fidelity signals such as access, session activity, assigned material usage, prompt volume, retrieval mode, and feature exposure.
- Avoid showing treatment labels, control labels, causal claims, or outcome comparisons during active study periods.
- Support exportable or queryable data needed by authorized research and operations workflows without making the teacher UI the primary research analysis environment.
- Make onboarding and first-use workflows short enough for teachers with low prior computer or AI exposure.
- Treat teacher motivation, school leadership buy-in, peer learning, and spillover between teachers as first-class implementation concerns.
- Support research-practice co-design so schools, teachers, implementation partners, and researchers can refine both the product and the implementation model.

Teacher-facing features that could change classroom behavior should be reviewed as part of the RCT implementation plan before release.

The initial pilot should allow observation of teacher uptake in realistic and even difficult conditions, including schools with low reported computer usage. If sample size permits later randomization, DeepGyan should be able to support teacher-only, student-only, and teacher-plus-student treatment arms.

## Rationale
Teachers are essential to classroom implementation. They need enough information to help students use DeepGyan successfully, but too much research-facing information can change behavior and threaten study validity.

Separating teacher-facing functionality from the student interface keeps student learning flows focused while giving educators the operational tools they need. It also creates a clean permission boundary for data access, reporting, and research exports.

Avoiding live outcome comparisons in the teacher UI helps reduce bias, differential encouragement, and informal changes in classroom practice during the trial.

The strongest technical capabilities will not matter if teachers do not adopt the tool. DeepGyan must therefore reduce planning burden, fit into the school day, respect teacher expertise, preserve teacher authority in front of students, and be easy enough for teachers to share with one another informally. Studying adoption mechanisms, including peer diffusion and school management support, is part of the product architecture rather than an external research concern.

Teacher-facing DeepGyan should enable better offline and classroom work, not simply increase screen time. Lesson plans and activities should help teachers create inquiry, paper-based work, group discussion, local examples, and hands-on learning where appropriate.

## Consequences
Positive consequences:

- Teachers get a purpose-built surface instead of relying on backend logs or student screens.
- The platform can support classroom operations and research fidelity without mixing those concerns into the student UI.
- Role boundaries make future permissions, exports, and audit requirements easier to implement.
- The pilot can study adoption, usability, peer spillover, school readiness, and infrastructure constraints before scaling.
- Evidence from a small number of schools can inform later ministry, municipality, grant, or larger implementation conversations.

Tradeoffs:

- Building teacher-facing views adds product scope beyond the current student dashboard.
- Some analytics that are useful after the RCT may need to stay hidden during active study periods.
- The platform will need clearer roles, classroom/group models, and access controls than the current minimal schema provides.
- Product design must spend engineering effort on onboarding, training support, and observability rather than only model features.
- School-level variation in infrastructure and leadership will complicate measurement and rollout.

## Implementation Notes
The teacher-facing surface should be implemented as a distinct dashboard route or application area, not as additional controls embedded into the student chat experience.

Future implementation work should add or preserve:

- Role-based access control for student, teacher, researcher, and administrator roles.
- Classroom, school, cohort, geography, infrastructure, and assignment models that can map to RCT study structures.
- Read-only instructional dashboards for usage, book progress, lesson plans created, classroom activities generated, common question themes, and technical access issues.
- Research-safe fidelity metrics that do not reveal treatment assignment or outcome comparisons to teachers.
- Export paths or database views for authorized research workflows.
- Logging that records teacher dashboard access and actions for auditability.
- Onboarding telemetry for account creation, first successful plan, repeated use, time-to-value, and abandoned flows.
- Support for pilot notes about school leadership, device availability, electricity/connectivity, and computer lab access.
- Feature flags for teacher-only, student-only, teacher-plus-student, and enhanced-support conditions.
- Mechanisms to observe peer diffusion, such as invitations, shared lesson plans, school-level adoption events, or training cohorts.
- Localization metadata for curriculum, grade, language, region, examples, and teacher preferences.
- Evaluation hooks for correctness, grounding, safety, cultural alignment, and curriculum relevance of generated plans and activities.

## Non-Goals
This ADR does not define the full teacher dashboard UI, research data dictionary, institutional review process, grant strategy, government engagement plan, or final RCT protocol. It records the architectural decision to treat teacher-facing functionality as the first pilot-ready, permissioned support surface with study-aware constraints.
