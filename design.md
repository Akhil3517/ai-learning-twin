# AI Skill Acceleration Platform - Design Document

## Overview

AI-powered learning platform that detects false confidence, generates adaptive roadmaps, and provides multilingual code mentoring. Built for 2-4 week hackathon MVP targeting India's developer workforce.

## Architecture

### System Architecture

```
                    ┌─────────────────────────────────────┐
                    │         USER INTERFACES             │
                    │  React Web App  |  VS Code + Q      │
                    └──────────────┬──────────────────────┘
                                   │
                    ┌──────────────▼──────────────────────┐
                    │      API Gateway + Cognito          │
                    └──────────────┬──────────────────────┘
                                   │
        ┏━━━━━━━━━━━━━━━━━━━━━━━━━▼━━━━━━━━━━━━━━━━━━━━━━━━━┓
        ┃          SERVICE LAYER (Lambda)                   ┃
        ┃  ┌──────────────┐  ┌──────────────┐  ┌─────────┐  ┃
        ┃  │  Learning    │  │     IDE      │  │Analytics│  ┃
        ┃  │ Orchestrator │  │  Assistant   │  │ Engine  │  ┃
        ┃  └──────┬───────┘  └──────┬───────┘  └────┬────┘  ┃
        ┗━━━━━━━━━┿━━━━━━━━━━━━━━━━┿━━━━━━━━━━━━━━━┿━━━━━━━━┛
                  │                 │                │
        ┏━━━━━━━━━▼━━━━━━━━━━━━━━━━━▼━━━━━━━━━━━━━━━━▼━━━━━┓
        ┃                                                  ┃
        ┃     ╔═══════════════════════════════════════╗    ┃
        ┃     ║   AI INTELLIGENCE ENGINE (Bedrock)    ║    ┃
        ┃     ║                                       ║    ┃
        ┃     ║   ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓    ║    ┃
        ┃     ║   ┃ ⭐FALSE CONFIDENCE ENGINE ⭐┃    ║    ┃
        ┃     ║   ┗━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━┛    ║    ┃
        ┃     ║                 │                     ║    ┃
        ┃     ║   ┏━━━━━━━━━━━━━▼━━━━━━━━━━━━━━━┓     ║    ┃
        ┃     ║   ┃ ⭐ LEARNING TWIN ⭐        ┃     ║    ┃
        ┃     ║   ┗━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━┛     ║    ┃
        ┃     ║                 │                     ║    ┃
        ┃     ║   ┏━━━━━━━━━━━━━▼━━━━━━━━━━━━━━━┓     ║    ┃
        ┃     ║   ┃ ⭐ SKILL GAP ANALYZER ⭐   ┃     ║    ┃
        ┃     ║   ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛     ║    ┃
        ┃     ║                                       ║    ┃
        ┃     ║   [L1→L2→L3]  [Question Gen]          ║    ┃
        ┃     ╚═══════════════════════════════════════╝    ┃
        ┃                                                  ┃
        ┗━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                              │
        ┏━━━━━━━━━━━━━━━━━━━━━▼━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
        ┃              DATA LAYER (DynamoDB)              ┃
        ┃   ╔═══════╗  ╔═══════╗  ╔═══════╗  ╔═════════╗  ┃
        ┃   ║ Twin  ║  ║Session║  ║Roadmap║  ║ NIELIT+ ║  ┃
        ┃   ║  DB   ║  ║  DB   ║  ║  DB   ║  ║Market DB║  ┃
        ┃   ╚═══════╝  ╚═══════╝  ╚═══════╝  ╚═════════╝  ┃
        ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

### Architecture Components

**Frontend**: React web app + VS Code extension (Amazon Q integration)
**API Layer**: API Gateway (routing, rate limiting) + Cognito (auth)
**Service Layer**: Lambda functions for orchestration, IDE assistance, analytics
**AI Engine**: Bedrock-powered intelligence with 3 core innovations
**Data Layer**: DynamoDB for real-time state, session logs, roadmap config

### Expected Impact Metrics

**Learning Outcomes:**
- 35% reduction in dropout rate (early struggle detection + intervention)
- 40% improvement in confidence calibration accuracy (FC < 0.2 delta)
- 25% faster skill acquisition velocity (adaptive pacing + remediation)

**Engagement:**
- 50% reduction in time spent on mastered content (fast-tracking)
- 60% increase in L2→L3 progression success rate (overconfidence prevention)
- 3x more accurate self-assessment after 10 sessions (FC convergence)

**Business Value:**
- 30% higher job placement rate (NIELIT + market alignment)
- 45% reduction in false confidence incidents in production code
- 2x improvement in learner retention (personalized adaptive paths)

### Service Layer (Lambda Functions)

**Learning Orchestrator**: 
- Roadmap generation with job role alignment
- Session management and performance signal capture
- Multilingual content translation (Hindi/Tamil/Telugu/Marathi)
- FC evaluation triggering

**IDE Assistant**: 
- VS Code integration via Amazon Q
- Real-time code analysis (intent vs implementation)
- Inline hints and explanations
- Learning Twin state updates from coding patterns

**Analytics Engine**: 
- Platform metrics and learning outcome tracking
- Job market trend aggregation (via Amazon Q)
- Dropout prediction and intervention
- Roadmap relevance updates

### AI Intelligence Engine (Core Innovation - Bedrock Powered)

**⭐ FALSE CONFIDENCE ENGINE ⭐** (Primary Innovation)
- Calculates FC score: `FalseConfidence = SelfConfidence - PerformanceScore`
- Performance Score: `PS = 0.35×quiz + 0.20×debug_efficiency + 0.20×hint_independence + 0.15×code_quality + 0.10×reattempt_penalty`
- Threshold logic: FC > 0.3 → Overconfidence (block), FC < -0.3 → Underconfidence (fast-track)
- Gates L1→L2→L3 progression based on calibration
- Triggers remediation or acceleration paths

**⭐ LEARNING TWIN ⭐** (Adaptive Intelligence)
- Maintains per-skill mastery scores (exponential moving average)
- Tracks learning velocity (skills/hour) and cognitive load
- Stores FC delta history for trend analysis
- Adapts roadmap dynamically based on performance patterns
- Predicts struggle points and optimal learning paths
- Roadblock prediction: Lightweight logistic regression or LLM-based reasoning estimates failure probability using learning velocity and calibration delta

**⭐ SKILL GAP ANALYZER ⭐** (Job Market Alignment)
- Compares current mastery vs target job requirements
- Identifies priority learning gaps with NIELIT curriculum alignment
- Estimates time to proficiency based on learning velocity
- Generates personalized skill roadmaps with dependencies

**Supporting Components:**
- **L1→L2→L3 Engine**: Enforces level-based progression, blocks advancement if FC > threshold
- **Question Generator**: Creates adaptive questions (basic, scenario-based, failure-at-scale)

### Data Layer

**Learning Twin DB (DynamoDB)**: UserLearningTwin state (mastery, confidence, velocity per skill)
**Session History DB (DynamoDB)**: Quiz results, time spent, hints used, error rates, reattempts
**Roadmap Config DB (DynamoDB)**: Skill dependencies, job role requirements, progression rules
**NIELIT + Market DB (DynamoDB)**: Curriculum data, certification paths, job market trends (updated periodically)

## Data Models

```typescript
// UserLearningTwin
{
  userId: string,
  skills: { [topicId: string]: {
    masteryScore: float, confidenceScore: float,
    falseConfidenceDelta: float, learningVelocity: float, lastUpdated: timestamp
  }},
  preferredLearningStyle: string, cognitiveLoadIndex: float
}

// SkillNode
{ topicId: string, name: string, nielitAligned: boolean, 
  dependencies: string[], estimatedHours: float, difficultyLevel: 1|2|3 }

// LearningSession
{ sessionId: string, userId: string, topicId: string, quizAccuracy: float,
  timeSpent: float, hintsUsed: int, errorRate: float, reattemptCount: int,
  selfRatedConfidence: float, timestamp: timestamp }
```

## False Confidence Engine

**Input Signals**: Self-rated confidence (1-5), quiz accuracy, time taken, hint usage, error rate, reattempt count

**Feature Vector**: `F = [normalized_quiz_score, normalized_debug_time, hint_independence_score, code_quality, reattempt_penalty]`

**Performance Score**: `PS = 0.35×quiz + 0.20×debug_efficiency + 0.20×hint_independence + 0.15×code_quality + 0.10×reattempt_penalty`

**False Confidence**: `FC = SelfConfidence - PS`

**Thresholds**: FC > 0.3 → Overconfidence (block), FC < -0.3 → Underconfidence (fast-track), Otherwise → Calibrated

**Progression Gates**: L1→L2 requires FC < 0.3, L2→L3 requires FC < 0.2

## System Flows

**Learning Session**: User starts session → Lambda fetches Twin → Bedrock generates questions → User completes quiz → FC Engine calculates score → If FC > 0.3: block + remediation, else update Twin + unlock next → Store in DynamoDB

**IDE Assistance**: Developer writes code → Amazon Q captures context → Lambda sends to Bedrock → Bedrock analyzes intent vs implementation → Returns multilingual hints → Updates Learning Twin

**Confidence Evaluation**: User completes activity → System collects signals → FC Engine constructs feature vector → Calculates PS and FC → Applies threshold logic → Updates Twin → Triggers adaptive action

## Key Components

**Roadmap Generator**: Takes job role, skill level, time availability → Outputs ordered SkillNodes with timeline using topological sort

**Skill Gap Analyzer**: Compares UserLearningTwin vs job requirements → Outputs priority-ranked gaps with estimated hours

**False Confidence Engine**: Takes LearningSession data → Outputs FC score, progression decision, remediation plan

**Learning Twin Updater**: Takes session results, FC score → Updates UserLearningTwin using exponential moving average

**Multilingual Translator**: Takes English explanation, target language → Outputs culturally-aware translation (Hindi/Tamil/Telugu/Marathi)

## AI Inference Pipeline

```
User Input → Context Enrichment (Twin + History) → Bedrock Inference 
(Code Analysis | Question Generation | Explanation) → Post-Processing 
(FC Calculation | Twin Update | Adaptive Decision) → Response Delivery
```

## MVP Scope

**Included**: Adaptive roadmaps for 3 job roles, FC Engine with L1/L2 gates, Basic Learning Twin, Web app with quiz interface, Bedrock integration, DynamoDB storage

**Simulated**: L3 scenarios (pre-built), Multilingual (English + Hindi only), IDE extension (mockup), Amazon Q data (static)

**Future**: Full multilingual support, Production IDE extension, Advanced Twin analytics, NIELIT lab integration, Mobile app

## Error Handling & Testing

**Errors**: Invalid Input (400), Bedrock Timeout (retry 3x + fallback), DynamoDB Failure (503 + queue), FC Error (default FC=0)

**Testing**: Unit tests (mocked dependencies), Property tests (100+ sessions), Integration tests (end-to-end), Load tests (1000 concurrent users)

## Correctness Properties

1. **FC Monotonicity**: For improving quiz scores, FC delta decreases over time
2. **Roadmap Completeness**: Generated roadmaps include all prerequisite skills in dependency order
3. **Multilingual Consistency**: Translations preserve code snippets and technical terms
4. **Twin Convergence**: Mastery scores converge to stable values after sufficient practice
5. **Progression Gate Enforcement**: Users with FC > 0.3 are blocked from L1→L2 progression
