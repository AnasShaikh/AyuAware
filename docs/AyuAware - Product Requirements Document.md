# **AyuAware \- Product Requirements Document** {#ayuaware---product-requirements-document}

**Version:** 1.0  
**Date:** January 2026  
**Status:** Draft for MVP Development

---

## **Document Overview** {#document-overview}

This Product Requirements Document (PRD) defines the complete specification for AyuAware, an Ayurvedic digital health companion that combines 5,000 years of Ayurvedic wisdom with modern AI technology.

**Purpose:** Guide development of a personalized health application that analyzes multi-modal health data and provides evidence-based Ayurvedic guidance.

**Scope:** Complete application including chat interface, health data analysis, protocol generation, educational content, and e-commerce integration.

---

##              **Table of Contents** {#table-of-contents}

[AyuAware \- Product Requirements Document](#ayuaware---product-requirements-document)

[Document Overview](#document-overview)

[Table of Contents](#table-of-contents)

[Core Building Blocks](#core-building-blocks)

[Digital Twin](#digital-twin)

[Fundamentals](#fundamentals)

[Constitution (Prakriti)](#constitution-\(prakriti\))

[Current State (Vikriti)](#current-state-\(vikriti\))

[Health Data Streams](#health-data-streams)

[Conversation Memory](#conversation-memory)

[Ayurvedic Intelligence Layer](#ayurvedic-intelligence-layer)

[Protocol Engine](#protocol-engine)

[Health Interactions](#health-interactions)

[Morning Summary](#morning-summary)

[Daily Check-In](#daily-check-in)

[Scan Analysis](#scan-analysis)

[Health Query](#health-query)

[Protocol Request](#protocol-request)

[Prediction Alert](#prediction-alert)

[Protocol Structure](#protocol-structure)

[Protocol Components](#protocol-components)

[Protocol Tracking](#protocol-tracking)

[Knowledge Base](#knowledge-base)

[Structured Ayurvedic Knowledge](#structured-ayurvedic-knowledge)

[User-Specific Knowledge](#user-specific-knowledge)

[Safety Boundaries](#safety-boundaries)

[Apps & Interfaces](#apps-&-interfaces)

[Main Chat Interface (Primary Screen)](#main-chat-interface-\(primary-screen\))

[Header](#header)

[Chat Area](#chat-area)

[Message Types](#message-types)

[Input Area (Bottom)](#input-area-\(bottom\))

[Voice Mode](#voice-mode)

[Navigation Drawer (Hamburger Menu)](#navigation-drawer-\(hamburger-menu\))

[Menu Structure](#menu-structure)

[1\. Today / History](#1.-today-/-history)

[Today Tab (Default)](#today-tab-\(default\))

[Morning Summary Card](#morning-summary-card)

[Current Status Snapshot](#current-status-snapshot)

[Today's Actions](#today's-actions)

[Quick Stats](#quick-stats)

[History Tab](#history-tab)

[Search & Filters](#search-&-filters)

[Conversation Timeline](#conversation-timeline)

[Favorites/Bookmarks](#favorites/bookmarks)

[2\. My Twin](#2.-my-twin)

[My Twin Profile](#my-twin-profile)

[Digital Twin Identity](#digital-twin-identity)

[What My Twin Knows About Me](#what-my-twin-knows-about-me)

[Customize My Twin](#customize-my-twin)

[Communication Settings](#communication-settings)

[Voice Settings](#voice-settings)

[Notification Preferences](#notification-preferences)

[Data Access Permissions](#data-access-permissions)

[3\. Insights](#3.-insights)

[Health Tab](#health-tab)

[Dosha Balance Section](#dosha-balance-section)

[Agni (Digestive Fire) Section](#agni-\(digestive-fire\)-section)

[Ama (Toxins) Section](#ama-\(toxins\)-section)

[Ojas (Vitality) Meter](#ojas-\(vitality\)-meter)

[Recent Lab Results](#recent-lab-results)

[Vital Signs](#vital-signs)

[Symptom Tracker](#symptom-tracker)

[Sleep Analysis](#sleep-analysis)

[Cycle Tracking (menstruating users)](#cycle-tracking-\(menstruating-users\))

[Mental/Emotional Health](#mental/emotional-health)

[Exposure Tab](#exposure-tab)

[Environmental Factors](#environmental-factors)

[Substance Exposure](#substance-exposure)

[Stress Events](#stress-events)

[Sleep Environment](#sleep-environment)

[Social & Activity Patterns](#social-&-activity-patterns)

[Nutrition Tab](#nutrition-tab)

[Daily Food Log](#daily-food-log)

[Six Tastes Analysis](#six-tastes-analysis)

[Dosha Impact Tracking](#dosha-impact-tracking)

[Meal Timing & Agni](#meal-timing-&-agni)

[Food Quality Metrics](#food-quality-metrics)

[Hydration Tracking](#hydration-tracking)

[Food Sensitivities](#food-sensitivities)

[Supplement Tab](#supplement-tab)

[Current Supplements](#current-supplements)

[Ayurvedic Herbs](#ayurvedic-herbs)

[Vitamins & Minerals](#vitamins-&-minerals)

[Medication Interactions](#medication-interactions)

[Effectiveness Tracking](#effectiveness-tracking)

[Lifestyle Tab](#lifestyle-tab)

[Daily Routine (Dinacharya)](#daily-routine-\(dinacharya\))

[Sleep Patterns](#sleep-patterns)

[Exercise & Movement](#exercise-&-movement)

[Meditation & Mindfulness](#meditation-&-mindfulness)

[Pranayama (Breathwork)](#pranayama-\(breathwork\))

[Yoga Practice](#yoga-practice)

[Self-Care Practices](#self-care-practices)

[4\. Protocols Section](#4.-protocols-section)

[Active Protocols View](#active-protocols-view)

[Primary Active Protocol](#primary-active-protocol)

[Today's Recommendations](#today's-recommendations)

[Progress Section](#progress-section)

[Protocol Details View](#protocol-details-view)

[Overview](#overview)

[Current Phase](#current-phase)

[All Recommendations](#all-recommendations)

[Rationale Section](#rationale-section)

[Tracking Interface](#tracking-interface)

[Protocol Library](#protocol-library)

[Browse Protocols](#browse-protocols)

[Featured Protocols](#featured-protocols)

[Past Protocols](#past-protocols)

[5\. Projects Section](#5.-projects-section)

[Active Projects](#active-projects)

[Project Detail View](#project-detail-view)

[Project Overview](#project-overview)

[Project Timeline](#project-timeline)

[Multi-Protocol Sequence](#multi-protocol-sequence)

[Progress Tracking](#progress-tracking)

[Journal & Reflections](#journal-&-reflections)

[Milestones & Celebrations](#milestones-&-celebrations)

[Provider Collaboration](#provider-collaboration)

[6\. Learn Section](#6.-learn-section)

[Learning Dashboard](#learning-dashboard)

[Learning Paths](#learning-paths)

[Lesson Structure](#lesson-structure)

[Interactive Features](#interactive-features)

[7\. Shop Section](#7.-shop-section)

[Product Categories](#product-categories)

[Product Details](#product-details)

[8\. Profile](#8.-profile)

[Sections](#sections)

[Tools & Actions](#tools-&-actions)

[Visual Builder](#visual-builder)

[Data Privacy & Security](#data-privacy-&-security)

[Integrations](#integrations)

[Authentication & Permissions](#authentication-&-permissions)

[Pricing](#pricing)

[Error Handling](#error-handling)

[Logical Flow: AI-Guided Setup](#logical-flow:-ai-guided-setup)

[Testing & Quality Assurance](#testing-&-quality-assurance)

## 

---

#                **Core Building Blocks** {#core-building-blocks}

## **Digital Twin** {#digital-twin}

AI-powered Ayurvedic health companion that represents the user's complete health profile. The Digital Twin intelligently converses with users, analyzes multi-modal health data, generates personalized protocols, and provides predictive health insights based on 5,000 years of Ayurvedic wisdom combined with modern health science.

### **Fundamentals** {#fundamentals}

#### **Constitution (Prakriti)** {#constitution-(prakriti)}

User's birth constitution determined through comprehensive assessment. Immutable baseline representing natural dosha balance (Vata-Pitta-Kapha percentages).

#### **Current State (Vikriti)** {#current-state-(vikriti)}

Dynamic health state reflecting current dosha imbalances. Updated through continuous data integration and user check-ins.

#### **Health Data Streams** {#health-data-streams}

Multi-modal inputs that inform the Digital Twin:

* **Wearable Data**: Sleep patterns, HRV, activity, heart rate, body temperature  
* **Lab Results**: Blood work, hormone panels, metabolic markers  
* **Genetic Data**: DNA variants affecting constitution and health predispositions  
* **Visual Diagnostics**: Tongue, skin, nail analysis through image uploads  
* **Questionnaires**: Symptom checklists, lifestyle assessments, daily check-ins  
* **Manual Logs**: Meals, symptoms, menstrual cycles, meditation practice

#### **Conversation Memory** {#conversation-memory}

Persistent context across all interactions. Digital Twin remembers user's health journey, preferences, past protocols, what worked/didn't work.

#### **Ayurvedic Intelligence Layer** {#ayurvedic-intelligence-layer}

Core knowledge system including:

* Dosha principles and characteristics  
* Agni (digestive fire) states  
* Ama (toxin) assessment frameworks  
* Food qualities and combinations  
* Herbal monographs (500+ herbs)  
* Seasonal routines (Ritucharya)  
* Daily routines (Dinacharya)  
* Constitutional dietary guidelines  
* Symptom-to-dosha correlation matrices

#### **Protocol Engine** {#protocol-engine}

Generates personalized wellness plans based on:

* User's constitution and current imbalances  
* Integrated health data patterns  
* Seasonal/environmental factors  
* Lifestyle constraints and preferences  
* Evidence-based Ayurvedic interventions

### **Health Interactions** {#health-interactions}

#### **Morning Summary** {#morning-summary}

Automated daily greeting synthesizing overnight data, providing dosha forecast, and recommending top 3 actions for the day.

#### **Daily Check-In** {#daily-check-in}

Quick health status assessment through conversational interface or structured forms. Tracks energy, sleep quality, digestion, mood, symptoms.

#### **Scan Analysis** {#scan-analysis}

Upload photos for instant Ayurvedic interpretation:

* **Tongue Scan**: Coating, color, texture, marks analyzed for Ama, Agni, and dosha status  
* **Meal Scan**: Food analysis for dosha effects, taste balance, appropriateness for constitution  
* **Product Scan**: Ingredient analysis for herbs, supplements, or packaged foods  
* **Skin Scan**: Complexion, texture, issues analyzed for dosha imbalances

#### **Health Query** {#health-query}

Natural conversation about any health topic. Digital Twin provides Ayurvedic perspective, explanations, and actionable guidance.

#### **Protocol Request** {#protocol-request}

User requests wellness plan for specific concern (sleep, digestion, stress, skin, energy, etc.). Digital Twin generates comprehensive, phased protocol.

#### **Prediction Alert** {#prediction-alert}

Proactive notifications when data patterns suggest impending imbalance. Preventive recommendations before symptoms manifest.

### **Protocol Structure** {#protocol-structure}

#### **Protocol Components** {#protocol-components}

* **Name & Duration**: Clear title and timeline (7-day, 21-day, 90-day, etc.)  
* **Primary Focus**: Target imbalances being addressed  
* **Phases**: Progressive approach (Foundation → Building → Maintenance)  
* **Recommendations by Category**:  
  * Dietary (foods to favor/avoid, meal timing, preparation methods)  
  * Lifestyle (daily routine, sleep schedule, stress management)  
  * Herbs & Supplements (specific recommendations with dosages, timing, cautions)  
  * Practices (yoga asanas, pranayama, meditation, self-massage)  
  * Environmental (seasonal adjustments, exposure management)  
* **Rationale**: WHY each recommendation matters (Ayurvedic explanation)  
* **Success Metrics**: What to track and expected improvements  
* **Check-in Schedule**: When Digital Twin will assess progress  
* **Adjustment Triggers**: Conditions that warrant protocol modification

#### **Protocol Tracking** {#protocol-tracking}

* Daily adherence logging (simple check-boxes for each recommendation)  
* Progress notes and observations  
* Symptom tracking over time  
* Before/after comparisons  
* Digital Twin provides encouragement and adjusts based on adherence

### **Knowledge Base** {#knowledge-base}

#### **Structured Ayurvedic Knowledge** {#structured-ayurvedic-knowledge}

* Classical texts excerpts (Charaka Samhita, Sushruta Samhita, Ashtanga Hridaya)  
* Dosha characteristics and qualities (complete matrices)  
* Six tastes with food databases (Rasa system)  
* Herb properties and uses (Dravyaguna)  
* Disease pathology (Samprapti)  
* Treatment principles (Chikitsa)  
* Constitutional assessment criteria  
* Seasonal wisdom and adjustments

#### **User-Specific Knowledge** {#user-specific-knowledge}

* Personal health history  
* Past protocols and outcomes  
* Food sensitivities and preferences  
* Lifestyle constraints  
* Goals and priorities  
* Provider information  
* Medication list  
* Family health history

#### **Safety Boundaries** {#safety-boundaries}

* Medical disclaimer framework  
* Emergency detection protocols  
* Scope limitations (what Digital Twin can/cannot address)  
* When to recommend medical consultation  
* Herb contraindications database  
* Drug-herb interaction warnings

---

#                **Apps & Interfaces** {#apps-&-interfaces}

## **Main Chat Interface (Primary Screen)** {#main-chat-interface-(primary-screen)}

Full-screen conversational interface with the Digital Twin. This is the default view and primary interaction point.

### **Header** {#header}

* **Left**: Hamburger menu icon (☰) \- opens navigation drawer  
* **Center**: "AyuAware" logo or user's custom Twin name  
* **Right**: Quick action buttons (Camera icon for Scan, Voice mode icon)

### **Chat Area** {#chat-area}

* Full-height scrollable conversation  
* Message bubbles with timestamps  
* Rich message types (text, cards, visualizations, quick actions)  
* Typing indicators when Digital Twin is responding  
* Scroll-to-bottom button when scrolled up

### **Message Types** {#message-types}

* **Text Response**: Natural conversational replies with Ayurvedic personality  
* **Summary Cards**: Expandable data visualizations (sleep summary, dosha forecast, etc.)  
* **Recommendation Lists**: Actionable guidance with rationale  
* **Educational Content**: Concept explanations with Sanskrit terms and translations  
* **Protocol Cards**: Full protocol preview with accept/modify options  
* **Data Visualizations**: Charts showing trends (HRV, dosha balance, symptom tracking)  
* **Quick Actions**: Buttons for common tasks

### **Input Area (Bottom)** {#input-area-(bottom)}

* Text input field with placeholder: "Ask your Digital Twin..."  
* Microphone icon (voice input)  
* Camera icon (quick scan access)  
* Attachment icon (upload images, documents)  
* Send button

### **Voice Mode** {#voice-mode}

* Tap microphone to activate full-screen voice interface  
* Waveform visualization showing Digital Twin's voice  
* Large tap-to-speak button  
* Hands-free conversation mode  
* Exit button returns to chat

---

## **Navigation Drawer (Hamburger Menu)** {#navigation-drawer-(hamburger-menu)}

Slides in from left when hamburger icon tapped.

### **Menu Structure** {#menu-structure}

1. **Today / History**  
2. **My Twin**  
3. **Insights** (with submenu)  
   * Health  
   * Exposure  
   * Nutrition  
   * Supplement  
   * Lifestyle  
4. **Protocols**  
5. **Projects**  
6. **Learn**  
7. **Shop**  
8. **Profile**

---

## **1\. Today / History** {#1.-today-/-history}

Combined view of current day summary and conversation history.

### **Today Tab (Default)** {#today-tab-(default)}

#### **Morning Summary Card** {#morning-summary-card}

* Greeting with today's date  
* Sleep quality from last night  
* Today's dosha forecast with visual gauge  
* Top 3 recommended actions  
* Weather/seasonal context

#### **Current Status Snapshot** {#current-status-snapshot}

* Dosha Balance mini gauge  
* Agni Status indicator  
* Ama Level progress bar  
* Energy Today rating  
* Active Protocols count

#### **Today's Actions** {#today's-actions}

* Active protocol recommendations with checkboxes  
* Scheduled check-ins or reminders  
* Pending scans or assessments

#### **Quick Stats** {#quick-stats}

* Days on current protocol  
* Check-in streak  
* This week's adherence percentage

### **History Tab** {#history-tab}

#### **Search & Filters** {#search-&-filters}

* Search all past conversations  
* Filter by: Topics, Protocols, Scans, Education

#### **Conversation Timeline** {#conversation-timeline}

* Organized by date  
* Conversation previews with highlights  
* Tap to open full conversation

#### **Favorites/Bookmarks** {#favorites/bookmarks}

* Saved important explanations  
* Quick access to frequently referenced topics

---

## **2\. My Twin** {#2.-my-twin}

Understand and customize your Digital Twin's personality and knowledge.

### **My Twin Profile** {#my-twin-profile}

#### **Digital Twin Identity** {#digital-twin-identity}

* Twin name (editable)  
* Visual avatar  
* Current communication style  
* Voice selection

#### **What My Twin Knows About Me** {#what-my-twin-knows-about-me}

**Constitutional Knowledge:**

* Prakriti with percentages  
* Last assessment date  
* Detailed constitution report link

**Current State Awareness:**

* Vikriti (current imbalances)  
* Recent patterns recognized  
* Last assessed date

**Health Goals & Priorities:**

* Listed goals  
* Priority ranking  
* Progress tracking

**Personal Preferences:**

* Dietary restrictions  
* Lifestyle constraints  
* Exercise preferences  
* Practice preferences

**Health History:**

* Medical conditions  
* Current medications  
* Allergies  
* Family history

**Interaction Memory:**

* Conversation count  
* Topics discussed  
* Protocols created  
* Success patterns

### **Customize My Twin** {#customize-my-twin}

#### **Communication Settings** {#communication-settings}

* Style: Supportive Friend / Wise Teacher / Clinical Guide  
* Verbosity: Brief / Balanced / Detailed  
* Sanskrit Usage: Minimal / Moderate / Extensive  
* Formality: Casual / Balanced / Formal

#### **Voice Settings** {#voice-settings}

* Voice selection  
* Speech speed  
* Personality in voice

#### **Notification Preferences** {#notification-preferences}

* Morning summary timing  
* Prediction alert sensitivity  
* Check-in reminders  
* Do Not Disturb hours

#### **Data Access Permissions** {#data-access-permissions}

* Which health data sources accessible  
* What data used for insights  
* Sharing permissions with practitioners

---

## **3\. Insights** {#3.-insights}

Comprehensive health data visualization across five categories.

### **Health Tab** {#health-tab}

#### **Dosha Balance Section** {#dosha-balance-section}

* Visual gauge (V-P-K percentages)  
* Comparison: Current vs. Constitutional baseline  
* Trend graph over time  
* Digital Twin's interpretation  
* Quick actions

#### **Agni (Digestive Fire) Section** {#agni-(digestive-fire)-section}

* Current status: Sama/Vishama/Tikshna/Manda  
* Assessment criteria  
* Trend over time  
* Recommendations

#### **Ama (Toxins) Section** {#ama-(toxins)-section}

* Current level: Low/Moderate/High  
* Indicators from tongue, digestion, energy  
* Recent scan timeline  
* Detox protocol status

#### **Ojas (Vitality) Meter** {#ojas-(vitality)-meter}

* Current vitality level  
* Contributing factors  
* Trend over time  
* Ojas-building recommendations

#### **Recent Lab Results** {#recent-lab-results}

* Latest upload date  
* Key biomarkers with Ayurvedic interpretations  
* Pattern analysis  
* Action buttons

#### **Vital Signs** {#vital-signs}

* Heart Rate, HRV, Blood Pressure  
* Weight, Body Temperature  
* Trends and correlations

#### **Symptom Tracker** {#symptom-tracker}

* Active symptoms mapped to doshas  
* Symptom timeline  
* Pattern recognition  
* Body map interface

#### **Sleep Analysis** {#sleep-analysis}

* Last night's sleep data  
* Sleep patterns and consistency  
* Dosha interpretation  
* 7-day trend  
* Recommendations

#### **Cycle Tracking (menstruating users)** {#cycle-tracking-(menstruating-users)}

* Current phase  
* Cycle day  
* Dosha correlation by phase  
* Symptom tracking  
* Predictions

#### **Mental/Emotional Health** {#mental/emotional-health}

* Current mood  
* Mood trends with dosha correlations  
* Stress level  
* Mental clarity assessment  
* Guna balance (Sattva-Rajas-Tamas)

### **Exposure Tab** {#exposure-tab}

#### **Environmental Factors** {#environmental-factors}

* Current weather and dosha impact  
* Air quality  
* Seasonal context  
* Lunar phase  
* Personalized recommendations

#### **Substance Exposure** {#substance-exposure}

* Caffeine log and effects  
* Alcohol log  
* Other substances  
* Dosha impact analysis

#### **Stress Events** {#stress-events}

* Timeline of stressors  
* Stress ratings  
* Physical correlations  
* Pattern recognition  
* Coping effectiveness

#### **Sleep Environment** {#sleep-environment}

* Bedroom conditions  
* Screen time before bed  
* Evening routine  
* Sleep hygiene score

#### **Social & Activity Patterns** {#social-&-activity-patterns}

* Social engagement levels  
* Work patterns  
* Travel log  
* Major life changes  
* Digital exposure

### **Nutrition Tab** {#nutrition-tab}

#### **Daily Food Log** {#daily-food-log}

* Today's meals with photos  
* Quick log methods  
* Meal timing analysis  
* Dosha impact

#### **Six Tastes Analysis** {#six-tastes-analysis}

* Today's taste balance  
* Taste deficiencies  
* Constitutional needs  
* Weekly trend

#### **Dosha Impact Tracking** {#dosha-impact-tracking}

* Daily dosha exposure  
* Weekly balance  
* Imbalance alerts  
* Adjustments needed

#### **Meal Timing & Agni** {#meal-timing-&-agni}

* Largest meal timing  
* Consistency tracking  
* Gaps between meals  
* Fasting windows

#### **Food Quality Metrics** {#food-quality-metrics}

* Organic vs. conventional  
* Processed foods frequency  
* Home-cooked vs. restaurant  
* Fresh vs. leftovers  
* Quality score

#### **Hydration Tracking** {#hydration-tracking}

* Daily water intake  
* Water temperature  
* Timing (with/between meals)  
* Constitutional needs

#### **Food Sensitivities** {#food-sensitivities}

* Known sensitivities  
* Reaction tracking  
* Pattern recognition  
* Elimination protocol status

### **Supplement Tab** {#supplement-tab}

#### **Current Supplements** {#current-supplements}

* Active supplement list  
* Dosage and frequency  
* Purpose and benefits  
* Adherence tracking

#### **Ayurvedic Herbs** {#ayurvedic-herbs}

* Constitutional herbs  
* Current recommendations  
* Herb monographs  
* Herb details

#### **Vitamins & Minerals** {#vitamins-&-minerals}

* Current vitamins  
* Dosage analysis  
* Deficiency tracking  
* Food vs. supplement

#### **Medication Interactions** {#medication-interactions}

* Current medications  
* Interaction checker  
* Warnings  
* Timing recommendations

#### **Effectiveness Tracking** {#effectiveness-tracking}

* Symptom monitoring  
* Before/after comparisons  
* Correlation analysis  
* Adjustment recommendations

### **Lifestyle Tab** {#lifestyle-tab}

#### **Daily Routine (Dinacharya)** {#daily-routine-(dinacharya)}

* Current routine  
* Consistency score  
* Optimal routine  
* Gap analysis  
* Recommendations

#### **Sleep Patterns** {#sleep-patterns}

* Sleep schedule  
* Duration and quality  
* Bedtime routine  
* Environment  
* Naps

#### **Exercise & Movement** {#exercise-&-movement}

* Activity log  
* Constitutional appropriateness  
* Timing and intensity  
* Recovery  
* Effects on health

#### **Meditation & Mindfulness** {#meditation-&-mindfulness}

* Practice log  
* Consistency tracking  
* Techniques used  
* Benefits observed  
* Recommendations by constitution

#### **Pranayama (Breathwork)** {#pranayama-(breathwork)}

* Practice log  
* Constitutional recommendations  
* Breathing patterns  
* Effects

#### **Yoga Practice** {#yoga-practice}

* Asana log  
* Constitutional suitability  
* Time of day  
* Integration with health

#### **Self-Care Practices** {#self-care-practices}

* Abhyanga frequency  
* Tongue scraping  
* Oil pulling  
* Other practices  
* Routine consistency

---

##         **4\. Protocols Section** {#4.-protocols-section}

Active and past wellness plans with progress tracking.

### **Active Protocols View** {#active-protocols-view}

#### **Primary Active Protocol** {#primary-active-protocol}

* Name and visual  
* Current phase  
* Days active / Total duration  
* Adherence percentage  
* Quick stats

#### **Today's Recommendations** {#today's-recommendations}

* Checklist by category  
* Checkboxes to mark complete  
* Tap for full details

#### **Progress Section** {#progress-section}

* Adherence graph  
* Symptom improvement  
* Data correlations  
* Milestone achievements

### **Protocol Details View** {#protocol-details-view}

#### **Overview** {#overview}

* Full protocol name  
* Target imbalances  
* Duration and phases  
* Expected outcomes

#### **Current Phase** {#current-phase}

* Phase description  
* Key focus areas  
* All recommendations

#### **All Recommendations** {#all-recommendations}

Organized by category:

* Dietary  
* Lifestyle  
* Herbs & Supplements  
* Practices  
* Environmental

#### **Rationale Section** {#rationale-section}

* WHY each recommendation  
* Ayurvedic principles  
* Mechanism of action

#### **Tracking Interface** {#tracking-interface}

* Daily checklist  
* Notes section  
* Symptom tracking  
* Photo comparison

### **Protocol Library** {#protocol-library}

#### **Browse Protocols** {#browse-protocols}

* By concern  
* By season  
* By dosha  
* By duration  
* By intensity

#### **Featured Protocols** {#featured-protocols}

* Recommended for you  
* Seasonal highlights  
* Most effective

#### **Past Protocols** {#past-protocols}

* Timeline of completed protocols  
* Outcomes and reflections  
* Reactivate option

---

##      **5\. Projects Section** {#5.-projects-section}

Long-term health goals and multi-protocol initiatives.

### **Active Projects** {#active-projects}

Each project card shows:

* Project name and icon  
* Start date and duration  
* Progress percentage  
* Current milestone

### **Project Detail View** {#project-detail-view}

#### **Project Overview** {#project-overview}

* Goal statement  
* Success metrics  
* Why this matters  
* Personal motivation

#### **Project Timeline** {#project-timeline}

* Visual timeline  
* Completed milestones  
* Current position  
* Upcoming milestones

#### **Multi-Protocol Sequence** {#multi-protocol-sequence}

* Phase 1, 2, 3 protocols  
* Status of each  
* Sequential progression

#### **Progress Tracking** {#progress-tracking}

* Metrics dashboard  
* Before/after comparisons  
* Correlations

#### **Journal & Reflections** {#journal-&-reflections}

* Project journal entries  
* Photo timeline  
* Measurement log

#### **Milestones & Celebrations** {#milestones-&-celebrations}

* Achieved milestones  
* Upcoming checkpoints

#### **Provider Collaboration** {#provider-collaboration}

* Shared providers  
* Provider notes  
* Integration with medical care

---

## **6\. Learn Section** {#6.-learn-section}

Gamified Ayurvedic education journey.

### **Learning Dashboard** {#learning-dashboard}

* Overall progress  
* Current level  
* Badges earned  
* Lessons completed  
* Learning streak

### **Learning Paths** {#learning-paths}

1. Foundations (required)  
2. Your Constitution  
3. Daily Rhythms  
4. Seasonal Living  
5. Food as Medicine  
6. Herbal Wisdom  
7. Mind-Body Practices  
8. Advanced Topics

### **Lesson Structure** {#lesson-structure}

Each lesson includes:

* Introduction (1 min)  
* Core content (3-5 min)  
* Interactive element (2-3 min)  
* Practical application (1-2 min)  
* Summary (1 min)

### **Interactive Features** {#interactive-features}

* Quizzes with feedback  
* Progress tracking  
* Badges and achievements  
* Personalized recommendations

---

##                            **7\. Shop Section** {#7.-shop-section}

Curated marketplace for Ayurvedic products.

### **Product Categories** {#product-categories}

* Herbs & Supplements  
* Herbal Teas & Tonics  
* Self-Care Products  
* Kitchen & Cooking  
* Books & Resources  
* Tools & Accessories

### **Product Details** {#product-details}

* High-quality photos  
* Detailed description  
* Ayurvedic analysis  
* Suitability for user  
* Quality & safety info  
* Reviews by constitution

---

## **8\. Profile** {#8.-profile}

Personal information and account management.

### **Sections** {#sections}

* Personal Information  
* My Constitution  
* Health Information  
* Dietary Preferences  
* Lifestyle Constraints  
* Goals & Priorities  
* Subscription & Billing  
* Notifications  
* Privacy & Security  
* Data & Exports  
* My Content  
* Achievements  
* Support & Feedback  
* Settings

---

# **Tools & Actions** {#tools-&-actions}

**Assessment Tools**

**Constitutional Assessment (Prakriti Quiz)**

* 60 questions across physical, mental, and lifestyle domains  
* Scoring algorithm produces dosha percentages  
* Visual representation of constitution  
* Detailed explanation of results  
* Saved to user profile permanently  
* Can be retaken for verification

Actions:

1. Present question set with multiple choice answers  
2. Score responses using Ayurvedic criteria matrices  
3. Calculate Vata, Pitta, Kapha percentages  
4. AI Generate personalized constitution explanation  
5. Save Data → User Profile (prakriti field)  
6. Show Message with results and interpretation  
7. Trigger Next Component → Personalized welcome and guidance

**Current State Assessment (Vikriti Check)**

* Symptom checklist (100+ symptoms organized by dosha)  
* Lifestyle factors assessment  
* Recent changes and triggers  
* Severity ratings  
* Duration tracking  
* Pattern recognition

Actions:

1. Present symptom checklist grouped by body system  
2. Collect lifestyle factors (diet, routine, stress, sleep, exercise)  
3. AI Generate vikriti analysis comparing to prakriti baseline  
4. Identify primary and secondary imbalances  
5. Detect root causes and triggers  
6. Save Data → User Profile (vikriti field, assessment timestamp)  
7. AI Generate immediate recommendations  
8. Show Message with analysis and top 3 actions  
9. Trigger Next Component → Detailed protocol offer or chat continuation

**Daily Check-In**

* Quick 5-question assessment  
* Energy (1-10 scale)  
* Sleep quality (1-10 scale)  
* Digestion state (Good/Variable/Sluggish/Burning)  
* Mood (Calm/Anxious/Irritable/Heavy/Mixed)  
* Any new symptoms (free text)

Actions:

1. Present daily questions with appropriate input types  
2. Timestamp response  
3. Save Data → Daily Check-Ins (time-series data)  
4. AI Generate pattern analysis (compare to recent check-ins)  
5. Update vikriti if significant changes detected  
6. Show Message with acknowledgment and quick tip  
7. Branch → If concerning pattern detected:  
   * AI Generate deeper analysis  
   * Show Message with concern and recommendation  
   * Offer protocol adjustment or practitioner consultation

**Image Analysis Tools**

**Tongue Analysis**

* Upload photo or capture with camera  
* AI vision analysis of coating, color, texture, shape, marks  
* Ayurvedic interpretation of findings  
* Ama assessment, Agni status, dosha indicators  
* Comparison to previous tongue photos (track changes)  
* Actionable recommendations

Actions:

1. Webhook → Accept image file  
2. AI Generate (with vision) → Detailed tongue description  
   * Coating: amount, color, location  
   * Color: pale/red/purple/yellow  
   * Texture: dry/moist/swollen/cracked  
   * Shape: teeth marks, size, specific marks  
3. AI Generate → Ayurvedic interpretation using tongue analysis framework  
   * Map findings to doshas  
   * Assess Ama level  
   * Evaluate Agni state  
   * Identify affected organs (if cracks/marks present)  
4. AI Generate → Recommendations (3-5 specific actions)  
5. Save Data → Visual Diagnostics (image, analysis, timestamp, ama\_level, agni\_state)  
6. Show Message → Complete analysis with findings, meaning, and recommendations  
7. Branch → If significant Ama detected:  
   * AI Generate detox protocol  
   * Show Message offering protocol  
8. Trigger Next Component → Return to chat with analysis integrated into conversation

**Meal Scan**

* Photo analysis of meal/food  
* Identify ingredients and preparation method  
* Six taste analysis (sweet, sour, salty, pungent, bitter, astringent)  
* Dosha effect assessment (increases/decreases Vata-Pitta-Kapha)  
* Constitutional appropriateness rating  
* Food combining evaluation  
* Suggestions for improvement

Actions:

1. Webhook → Accept meal image file  
2. AI Generate (with vision) → Identify foods, ingredients, preparation  
3. AI Generate → Assess six tastes present  
4. AI Generate → Calculate dosha effects using food qualities database  
5. AI Generate → Evaluate for user's constitution and current state  
6. AI Generate → Check food combining principles  
7. AI Generate → Provide feedback and improvement suggestions  
8. Save Data → Meal Log (image, analysis, timestamp, dosha\_impact)  
9. Show Message → Complete meal analysis with rating and suggestions  
10. Ask if user wants to log this as consumed (for dietary tracking)  
11. Branch → If consumed:  
    * Save Data → Update daily dosha exposure metrics  
    * Update Agni tracking based on meal appropriateness

**Product Scan**

* Scan ingredient label or supplement facts  
* Extract ingredient list and dosages  
* Analyze each ingredient from Ayurvedic perspective  
* Check for contraindications based on user's constitution, current medications, health conditions  
* Quality assessment (if product in database)  
* Overall recommendation (Excellent/Good/Moderate/Avoid for this user)

Actions:

1. Webhook → Accept product image or manual ingredient input  
2. AI Generate (with vision if image) → Extract ingredient list  
3. AI Generate → Analyze each ingredient:  
   * Ayurvedic properties (rasa, virya, vipaka, prabhav)  
   * Dosha effects  
   * Therapeutic uses  
   * Safety profile  
4. Check contraindications against user profile (constitution, medications, conditions)  
5. AI Generate → Overall assessment for this specific user  
6. Save Data → Product Scans (product, analysis, recommendation, timestamp)  
7. Show Message → Ingredient-by-ingredient analysis and final recommendation  
8. Branch → If concerns detected:  
   * Show Message with specific warnings  
   * Suggest alternatives

**Skin Analysis** (V2)

* Facial photo analysis  
* Assess skin type (Vata/Pitta/Kapha characteristics)  
* Identify issues (dryness, oiliness, acne, redness, discoloration)  
* Map to dosha imbalances  
* Skincare protocol recommendations

Actions: Similar to tongue analysis but focused on skin assessment

**Data Integration Tools**

**Wearable Sync**

* Connect to Apple Health, Google Fit, Fitbit, Oura, WHOOP, Garmin  
* Pull sleep data, activity data, heart rate, HRV, body temperature  
* Transform into Ayurvedic insights  
* Automated sync (hourly or real-time)

Actions:

1. Webhook → Receive wearable data (OAuth authenticated)  
2. Save Data → Raw health metrics (sleep stages, steps, heart rate, HRV, etc.)  
3. AI Generate → Interpret sleep through dosha lens:  
   * Fragmented sleep \= Vata  
   * Night awakenings 10pm-2am \= Pitta  
   * Excessive sleep \= Kapha  
4. AI Generate → Assess HRV patterns (declining HRV \= stress, imbalance approaching)  
5. AI Generate → Activity appropriateness (too intense/too little for constitution)  
6. Update vikriti if patterns indicate dosha shifts  
7. Save Data → Dosha Activity Metrics (derived insights)  
8. Branch → If concerning pattern detected:  
   * Create prediction alert  
   * Send notification to user  
   * Prepare proactive recommendations

**Lab Results Upload**

* PDF or image upload of blood work, hormone panels, etc.  
* OCR to extract biomarker names and values  
* Reference ranges comparison  
* Ayurvedic interpretation of each marker  
* Pattern synthesis across multiple markers  
* Root cause analysis  
* Comprehensive protocol generation

Actions:

1. Webhook → Accept lab result PDF/image  
2. AI Generate (with vision) → Extract all biomarkers, values, reference ranges  
3. For each biomarker:  
   * AI Generate → Ayurvedic interpretation  
   * Map to tissue layers (dhatus)  
   * Connect to dosha imbalances  
4. AI Generate → Synthesize overall pattern  
5. AI Generate → Root cause analysis  
6. AI Generate → Comprehensive recommendations (diet, lifestyle, herbs)  
7. Save Data → Lab Results (all biomarkers, interpretations, date)  
8. Show Message → Complete analysis with priorities and protocol  
9. Branch → If critical values detected:  
   * Flag for medical consultation  
   * Urgent recommendation to see doctor

**Genetic Upload** (V2)

* Upload 23andMe, Ancestry DNA, or similar raw data  
* Parse genetic variants (MTHFR, COMT, inflammation genes, etc.)  
* Correlate to constitutional predispositions  
* Identify metabolic tendencies  
* Personalize protocols based on genetics

Actions: Similar to lab results but focused on genetic variants and constitutional validation

**Protocol Generation Tools**

**Create Protocol**

* Primary concern identification  
* Assessment of contributing factors  
* Phased protocol development  
* Multi-category recommendations  
* Rationale for each recommendation  
* Timeline and milestones  
* Success metrics definition

Actions:

1. Webhook → Receive protocol request (concern, duration, intensity, constraints)  
2. AI Generate → Analyze user's complete profile:  
   * Constitution and current imbalances  
   * Recent health data trends  
   * Active symptoms  
   * Lifestyle constraints  
   * Past protocol outcomes  
3. AI Generate → Design protocol structure:  
   * Define phases (Foundation/Building/Maintenance)  
   * Set duration for each phase  
   * Determine intensity level  
4. AI Generate → Create recommendations by category:  
   * Dietary (using food database for constitution)  
   * Lifestyle (routines aligned with doshas)  
   * Herbs (appropriate for imbalances, check contraindications)  
   * Practices (yoga, pranayama, meditation)  
   * Environmental adjustments  
5. For each recommendation:  
   * AI Generate rationale (WHY it matters in Ayurvedic terms)  
   * Define frequency/timing  
   * Add tips for success  
6. AI Generate → Success metrics and check-in schedule  
7. Save Data → Protocols (complete protocol object)  
8. Show Message → Present protocol with option to accept, modify, or discuss further  
9. Branch → If accepted:  
   * Save Data → Mark as active protocol  
   * Set up check-in reminders  
   * Initialize tracking interface  
10. Trigger Next Component → Protocol tracking dashboard

**Adjust Protocol**

* Based on adherence data  
* Based on progress metrics  
* Based on user feedback  
* Based on changing seasons/circumstances  
* Maintains protocol continuity while optimizing

Actions:

1. Webhook → Receive adjustment trigger (poor adherence, insufficient progress, user request, seasonal change)  
2. Retrieve current protocol and tracking data  
3. AI Generate → Analyze why adjustment needed  
4. AI Generate → Propose modifications:  
   * Simplify if adherence is issue  
   * Intensify if progress plateau  
   * Adapt for season/circumstances  
   * Address side effects or challenges  
5. Show Message → Explain reasoning and proposed changes  
6. Get user approval  
7. Save Data → Update protocol with modifications, maintain version history  
8. Show Message → Confirmation and renewed commitment

**Communication Tools**

**Morning Summary Generator**

* Automated trigger at user's preferred time (default 7:00 AM)  
* Synthesizes overnight and recent data  
* Provides dosha forecast  
* Recommends top actions for the day

Actions:

1. Scheduled Trigger → Daily at user's morning time  
2. Retrieve overnight wearable data (sleep metrics)  
3. Retrieve current vikriti and recent trends  
4. Get weather, season, and environmental factors  
5. Check active protocols and today's recommendations  
6. AI Generate → Compose personalized morning summary:  
   * Warm greeting with user's name  
   * Sleep quality interpretation  
   * Today's dosha forecast (based on data \+ environment)  
   * Top 3 specific actions  
   * Encouragement and context  
7. Format as rich message with summary card  
8. Send notification  
9. Display in chat when user opens app

**Prediction Alert**

* Background monitoring of data patterns  
* Detects early warning signs of imbalance  
* Proactive notification with preventive recommendations

Actions:

1. Scheduled Trigger → Every 6 hours (background analysis)  
2. Retrieve recent health data (wearables, check-ins, logs)  
3. AI Generate → Pattern analysis:  
   * Compare current data to user's baselines  
   * Look for concerning trends (declining HRV, poor sleep patterns, increasing symptoms)  
   * Cross-reference with historical patterns ("This user's Vata spikes after 3+ days of stress")  
4. Branch → If prediction criteria met:  
   * AI Generate → Specific prediction with timeline  
   * AI Generate → Preventive recommendations (3-5 actions)  
   * Create alert object  
   * Send notification  
   * Show Message in chat when user opens app  
5. Save Data → Prediction Log (prediction, outcome, user actions taken)

**Educational Response**

* Triggered when user asks about Ayurvedic concepts  
* Provides clear explanation with analogies  
* Uses Sanskrit terms with translations  
* Personalizes to user's constitution  
* Offers practical application

Actions:

1. Webhook → Receive user question about Ayurvedic concept  
2. AI Generate → Identify concept being asked about  
3. Retrieve relevant knowledge from Ayurvedic database  
4. AI Generate → Compose educational response:  
   * Relatable analogy or metaphor  
   * Concept explanation in modern terms  
   * Sanskrit term with pronunciation and translation  
   * Personalization to user's constitution  
   * Practical application  
   * Offer to go deeper if interested  
5. Show Message → Educational content formatted for readability  
6. Branch → If user wants more detail:  
   * AI Generate deeper dive  
   * Link to relevant Learn section lessons

**Safety & Boundary Tools**

**Emergency Detection**

* Real-time monitoring of user messages for emergency keywords  
* Immediate escalation protocol

Actions:

1. Webhook → Every user message passes through safety check  
2. AI Generate → Analyze for emergency indicators:  
   * Chest pain, difficulty breathing  
   * Suicidal thoughts  
   * Severe symptoms  
   * Medical emergencies  
3. Branch → If emergency detected:  
   * Override normal flow  
   * Show Message → "I'm concerned about what you're describing. This requires immediate medical attention. Please call emergency services (911) or go to the emergency room right away."  
   * Log incident  
   * Notify safety team (if applicable)  
   * Do NOT provide health advice  
4. If no emergency, continue normal flow

**Medical Boundary Check**

* Evaluates user request against scope limits  
* Redirects to medical consultation when appropriate

Actions:

1. AI Generate → Assess if request is within Ayurvedic wellness scope  
2. Branch → If outside scope (disease diagnosis, medication dosing, serious conditions):  
   * Show Message with gentle boundary explanation  
   * Recommend appropriate medical professional  
   * Offer complementary Ayurvedic support if applicable  
3. If within scope, proceed with normal guidance

**Herb Safety Check**

* Validates herb recommendations against contraindications  
* Checks drug-herb interactions

Actions:

1. When herb is recommended, retrieve:  
   * User's current medications  
   * User's health conditions  
   * User's constitution and current state  
2. Query contraindications database  
3. Branch → If contraindication found:  
   * Remove or modify herb recommendation  
   * Show warning message with explanation  
   * Suggest alternative herbs  
4. If safe, proceed with recommendation plus appropriate disclaimer

---

#                **Visual Builder** {#visual-builder}

**Assessment Tools**

**Constitutional Assessment (Prakriti Quiz)**

* 60 questions across physical, mental, and lifestyle domains  
* Scoring algorithm produces dosha percentages  
* Visual representation of constitution  
* Detailed explanation of results  
* Saved to user profile permanently  
* Can be retaken for verification

Actions:

1. Present question set with multiple choice answers  
2. Score responses using Ayurvedic criteria matrices  
3. Calculate Vata, Pitta, Kapha percentages  
4. AI Generate personalized constitution explanation  
5. Save Data → User Profile (prakriti field)  
6. Show Message with results and interpretation  
7. Trigger Next Component → Personalized welcome and guidance

**Current State Assessment (Vikriti Check)**

* Symptom checklist (100+ symptoms organized by dosha)  
* Lifestyle factors assessment  
* Recent changes and triggers  
* Severity ratings  
* Duration tracking  
* Pattern recognition

Actions:

1. Present symptom checklist grouped by body system  
2. Collect lifestyle factors (diet, routine, stress, sleep, exercise)  
3. AI Generate vikriti analysis comparing to prakriti baseline  
4. Identify primary and secondary imbalances  
5. Detect root causes and triggers  
6. Save Data → User Profile (vikriti field, assessment timestamp)  
7. AI Generate immediate recommendations  
8. Show Message with analysis and top 3 actions  
9. Trigger Next Component → Detailed protocol offer or chat continuation

**Daily Check-In**

* Quick 5-question assessment  
* Energy (1-10 scale)  
* Sleep quality (1-10 scale)  
* Digestion state (Good/Variable/Sluggish/Burning)  
* Mood (Calm/Anxious/Irritable/Heavy/Mixed)  
* Any new symptoms (free text)

Actions:

1. Present daily questions with appropriate input types  
2. Timestamp response  
3. Save Data → Daily Check-Ins (time-series data)  
4. AI Generate pattern analysis (compare to recent check-ins)  
5. Update vikriti if significant changes detected  
6. Show Message with acknowledgment and quick tip  
7. Branch → If concerning pattern detected:  
   * AI Generate deeper analysis  
   * Show Message with concern and recommendation  
   * Offer protocol adjustment or practitioner consultation

**Image Analysis Tools**

**Tongue Analysis**

* Upload photo or capture with camera  
* AI vision analysis of coating, color, texture, shape, marks  
* Ayurvedic interpretation of findings  
* Ama assessment, Agni status, dosha indicators  
* Comparison to previous tongue photos (track changes)  
* Actionable recommendations

Actions:

1. Webhook → Accept image file  
2. AI Generate (with vision) → Detailed tongue description  
   * Coating: amount, color, location  
   * Color: pale/red/purple/yellow  
   * Texture: dry/moist/swollen/cracked  
   * Shape: teeth marks, size, specific marks  
3. AI Generate → Ayurvedic interpretation using tongue analysis framework  
   * Map findings to doshas  
   * Assess Ama level  
   * Evaluate Agni state  
   * Identify affected organs (if cracks/marks present)  
4. AI Generate → Recommendations (3-5 specific actions)  
5. Save Data → Visual Diagnostics (image, analysis, timestamp, ama\_level, agni\_state)  
6. Show Message → Complete analysis with findings, meaning, and recommendations  
7. Branch → If significant Ama detected:  
   * AI Generate detox protocol  
   * Show Message offering protocol  
8. Trigger Next Component → Return to chat with analysis integrated into conversation

**Meal Scan**

* Photo analysis of meal/food  
* Identify ingredients and preparation method  
* Six taste analysis (sweet, sour, salty, pungent, bitter, astringent)  
* Dosha effect assessment (increases/decreases Vata-Pitta-Kapha)  
* Constitutional appropriateness rating  
* Food combining evaluation  
* Suggestions for improvement

Actions:

1. Webhook → Accept meal image file  
2. AI Generate (with vision) → Identify foods, ingredients, preparation  
3. AI Generate → Assess six tastes present  
4. AI Generate → Calculate dosha effects using food qualities database  
5. AI Generate → Evaluate for user's constitution and current state  
6. AI Generate → Check food combining principles  
7. AI Generate → Provide feedback and improvement suggestions  
8. Save Data → Meal Log (image, analysis, timestamp, dosha\_impact)  
9. Show Message → Complete meal analysis with rating and suggestions  
10. Ask if user wants to log this as consumed (for dietary tracking)  
11. Branch → If consumed:  
    * Save Data → Update daily dosha exposure metrics  
    * Update Agni tracking based on meal appropriateness

**Product Scan**

* Scan ingredient label or supplement facts  
* Extract ingredient list and dosages  
* Analyze each ingredient from Ayurvedic perspective  
* Check for contraindications based on user's constitution, current medications, health conditions  
* Quality assessment (if product in database)  
* Overall recommendation (Excellent/Good/Moderate/Avoid for this user)

Actions:

1. Webhook → Accept product image or manual ingredient input  
2. AI Generate (with vision if image) → Extract ingredient list  
3. AI Generate → Analyze each ingredient:  
   * Ayurvedic properties (rasa, virya, vipaka, prabhav)  
   * Dosha effects  
   * Therapeutic uses  
   * Safety profile  
4. Check contraindications against user profile (constitution, medications, conditions)  
5. AI Generate → Overall assessment for this specific user  
6. Save Data → Product Scans (product, analysis, recommendation, timestamp)  
7. Show Message → Ingredient-by-ingredient analysis and final recommendation  
8. Branch → If concerns detected:  
   * Show Message with specific warnings  
   * Suggest alternatives

**Skin Analysis** (V2)

* Facial photo analysis  
* Assess skin type (Vata/Pitta/Kapha characteristics)  
* Identify issues (dryness, oiliness, acne, redness, discoloration)  
* Map to dosha imbalances  
* Skincare protocol recommendations

Actions: Similar to tongue analysis but focused on skin assessment

**Data Integration Tools**

**Wearable Sync**

* Connect to Apple Health, Google Fit, Fitbit, Oura, WHOOP, Garmin  
* Pull sleep data, activity data, heart rate, HRV, body temperature  
* Transform into Ayurvedic insights  
* Automated sync (hourly or real-time)

Actions:

1. Webhook → Receive wearable data (OAuth authenticated)  
2. Save Data → Raw health metrics (sleep stages, steps, heart rate, HRV, etc.)  
3. AI Generate → Interpret sleep through dosha lens:  
   * Fragmented sleep \= Vata  
   * Night awakenings 10pm-2am \= Pitta  
   * Excessive sleep \= Kapha  
4. AI Generate → Assess HRV patterns (declining HRV \= stress, imbalance approaching)  
5. AI Generate → Activity appropriateness (too intense/too little for constitution)  
6. Update vikriti if patterns indicate dosha shifts  
7. Save Data → Dosha Activity Metrics (derived insights)  
8. Branch → If concerning pattern detected:  
   * Create prediction alert  
   * Send notification to user  
   * Prepare proactive recommendations

**Lab Results Upload**

* PDF or image upload of blood work, hormone panels, etc.  
* OCR to extract biomarker names and values  
* Reference ranges comparison  
* Ayurvedic interpretation of each marker  
* Pattern synthesis across multiple markers  
* Root cause analysis  
* Comprehensive protocol generation

Actions:

1. Webhook → Accept lab result PDF/image  
2. AI Generate (with vision) → Extract all biomarkers, values, reference ranges  
3. For each biomarker:  
   * AI Generate → Ayurvedic interpretation  
   * Map to tissue layers (dhatus)  
   * Connect to dosha imbalances  
4. AI Generate → Synthesize overall pattern  
5. AI Generate → Root cause analysis  
6. AI Generate → Comprehensive recommendations (diet, lifestyle, herbs)  
7. Save Data → Lab Results (all biomarkers, interpretations, date)  
8. Show Message → Complete analysis with priorities and protocol  
9. Branch → If critical values detected:  
   * Flag for medical consultation  
   * Urgent recommendation to see doctor

**Genetic Upload** (V2)

* Upload 23andMe, Ancestry DNA, or similar raw data  
* Parse genetic variants (MTHFR, COMT, inflammation genes, etc.)  
* Correlate to constitutional predispositions  
* Identify metabolic tendencies  
* Personalize protocols based on genetics

Actions: Similar to lab results but focused on genetic variants and constitutional validation

**Protocol Generation Tools**

**Create Protocol**

* Primary concern identification  
* Assessment of contributing factors  
* Phased protocol development  
* Multi-category recommendations  
* Rationale for each recommendation  
* Timeline and milestones  
* Success metrics definition

Actions:

1. Webhook → Receive protocol request (concern, duration, intensity, constraints)  
2. AI Generate → Analyze user's complete profile:  
   * Constitution and current imbalances  
   * Recent health data trends  
   * Active symptoms  
   * Lifestyle constraints  
   * Past protocol outcomes  
3. AI Generate → Design protocol structure:  
   * Define phases (Foundation/Building/Maintenance)  
   * Set duration for each phase  
   * Determine intensity level  
4. AI Generate → Create recommendations by category:  
   * Dietary (using food database for constitution)  
   * Lifestyle (routines aligned with doshas)  
   * Herbs (appropriate for imbalances, check contraindications)  
   * Practices (yoga, pranayama, meditation)  
   * Environmental adjustments  
5. For each recommendation:  
   * AI Generate rationale (WHY it matters in Ayurvedic terms)  
   * Define frequency/timing  
   * Add tips for success  
6. AI Generate → Success metrics and check-in schedule  
7. Save Data → Protocols (complete protocol object)  
8. Show Message → Present protocol with option to accept, modify, or discuss further  
9. Branch → If accepted:  
   * Save Data → Mark as active protocol  
   * Set up check-in reminders  
   * Initialize tracking interface  
10. Trigger Next Component → Protocol tracking dashboard

**Adjust Protocol**

* Based on adherence data  
* Based on progress metrics  
* Based on user feedback  
* Based on changing seasons/circumstances  
* Maintains protocol continuity while optimizing

Actions:

1. Webhook → Receive adjustment trigger (poor adherence, insufficient progress, user request, seasonal change)  
2. Retrieve current protocol and tracking data  
3. AI Generate → Analyze why adjustment needed  
4. AI Generate → Propose modifications:  
   * Simplify if adherence is issue  
   * Intensify if progress plateau  
   * Adapt for season/circumstances  
   * Address side effects or challenges  
5. Show Message → Explain reasoning and proposed changes  
6. Get user approval  
7. Save Data → Update protocol with modifications, maintain version history  
8. Show Message → Confirmation and renewed commitment

**Communication Tools**

**Morning Summary Generator**

* Automated trigger at user's preferred time (default 7:00 AM)  
* Synthesizes overnight and recent data  
* Provides dosha forecast  
* Recommends top actions for the day

Actions:

1. Scheduled Trigger → Daily at user's morning time  
2. Retrieve overnight wearable data (sleep metrics)  
3. Retrieve current vikriti and recent trends  
4. Get weather, season, and environmental factors  
5. Check active protocols and today's recommendations  
6. AI Generate → Compose personalized morning summary:  
   * Warm greeting with user's name  
   * Sleep quality interpretation  
   * Today's dosha forecast (based on data \+ environment)  
   * Top 3 specific actions  
   * Encouragement and context  
7. Format as rich message with summary card  
8. Send notification  
9. Display in chat when user opens app

**Prediction Alert**

* Background monitoring of data patterns  
* Detects early warning signs of imbalance  
* Proactive notification with preventive recommendations

Actions:

1. Scheduled Trigger → Every 6 hours (background analysis)  
2. Retrieve recent health data (wearables, check-ins, logs)  
3. AI Generate → Pattern analysis:  
   * Compare current data to user's baselines  
   * Look for concerning trends (declining HRV, poor sleep patterns, increasing symptoms)  
   * Cross-reference with historical patterns ("This user's Vata spikes after 3+ days of stress")  
4. Branch → If prediction criteria met:  
   * AI Generate → Specific prediction with timeline  
   * AI Generate → Preventive recommendations (3-5 actions)  
   * Create alert object  
   * Send notification  
   * Show Message in chat when user opens app  
5. Save Data → Prediction Log (prediction, outcome, user actions taken)

**Educational Response**

* Triggered when user asks about Ayurvedic concepts  
* Provides clear explanation with analogies  
* Uses Sanskrit terms with translations  
* Personalizes to user's constitution  
* Offers practical application

Actions:

1. Webhook → Receive user question about Ayurvedic concept  
2. AI Generate → Identify concept being asked about  
3. Retrieve relevant knowledge from Ayurvedic database  
4. AI Generate → Compose educational response:  
   * Relatable analogy or metaphor  
   * Concept explanation in modern terms  
   * Sanskrit term with pronunciation and translation  
   * Personalization to user's constitution  
   * Practical application  
   * Offer to go deeper if interested  
5. Show Message → Educational content formatted for readability  
6. Branch → If user wants more detail:  
   * AI Generate deeper dive  
   * Link to relevant Learn section lessons

**Safety & Boundary Tools**

**Emergency Detection**

* Real-time monitoring of user messages for emergency keywords  
* Immediate escalation protocol

Actions:

1. Webhook → Every user message passes through safety check  
2. AI Generate → Analyze for emergency indicators:  
   * Chest pain, difficulty breathing  
   * Suicidal thoughts  
   * Severe symptoms  
   * Medical emergencies  
3. Branch → If emergency detected:  
   * Override normal flow  
   * Show Message → "I'm concerned about what you're describing. This requires immediate medical attention. Please call emergency services (911) or go to the emergency room right away."  
   * Log incident  
   * Notify safety team (if applicable)  
   * Do NOT provide health advice  
4. If no emergency, continue normal flow

**Medical Boundary Check**

* Evaluates user request against scope limits  
* Redirects to medical consultation when appropriate

Actions:

1. AI Generate → Assess if request is within Ayurvedic wellness scope  
2. Branch → If outside scope (disease diagnosis, medication dosing, serious conditions):  
   * Show Message with gentle boundary explanation  
   * Recommend appropriate medical professional  
   * Offer complementary Ayurvedic support if applicable  
3. If within scope, proceed with normal guidance

**Herb Safety Check**

* Validates herb recommendations against contraindications  
* Checks drug-herb interactions

Actions:

1. When herb is recommended, retrieve:  
   * User's current medications  
   * User's health conditions  
   * User's constitution and current state  
2. Query contraindications database  
3. Branch → If contraindication found:  
   * Remove or modify herb recommendation  
   * Show warning message with explanation  
   * Suggest alternative herbs  
4. If safe, proceed with recommendation plus appropriate disclaimer

---

#              **Data Privacy & Security** {#data-privacy-&-security}

**Encryption**

* **End-to-end encryption** for all health data at rest and in transit  
* **HIPAA-compliant data storage** using AWS HIPAA-eligible services (S3 with encryption, RDS with encryption, etc.)  
* **Encrypted backups** with separate key management (AWS KMS)  
* **TLS 1.3** for all data transmission  
* **Field-level encryption** for particularly sensitive data (genetics, medical conditions, medications)  
* **No data used for AI training** without explicit, informed consent  
* **Encryption at rest**: AES-256  
* **Encryption in transit**: TLS 1.3 with perfect forward secrecy

**User Control**

**Granular Privacy Settings:**

* Control what data Digital Twin can access:  
  * ☐ Wearable data (sleep, activity, HRV, etc.)  
  * ☐ Manual health logs (check-ins, symptoms)  
  * ☐ Lab results  
  * ☐ Genetic data  
  * ☐ Images (tongue, skin, meals)  
  * ☐ Location (for weather/seasonal context)  
  * ☐ Conversation history  
* Each data type individually toggleable  
* Explanation of how each data type improves recommendations

**Data Portability:**

* **Download complete health record** in multiple formats:  
  * JSON (machine-readable, complete data)  
  * PDF (human-readable health summary)  
  * CSV (for spreadsheet analysis)  
  * FHIR format (for medical record integration)  
* **Export options:**  
  * All data (complete archive)  
  * Specific date ranges  
  * Specific data types only  
  * Protocols and recommendations only  
* **Automated exports**: Schedule regular backups to personal cloud storage

**Selective Deletion:**

* **Delete specific data types:**  
  * All conversations (keep health data)  
  * All images (keep analyses)  
  * Specific time periods  
  * Individual protocols or projects  
  * Wearable data imports  
* **Granular conversation deletion**: Delete individual messages or conversations  
* **Right to be forgotten**: Complete account deletion removes all data within 30 days  
* **Soft delete period**: 30-day recovery window before permanent deletion

**Third-Party Sharing Controls:**

* **Provider sharing:**  
  * Choose exactly which data to share with each practitioner  
  * Time-limited access (e.g., 3 months)  
  * Revoke access instantly  
  * Audit log of what providers accessed when  
* **Integration controls:**  
  * Which wearables/apps can send data  
  * Which apps can read AyuAware data  
  * Revoke integration access anytime  
* **Family/caregiver access** (optional):  
  * Share read-only view with family members  
  * Emergency access for trusted contacts  
  * Granular permissions (e.g., can see protocols but not lab results)

**Anonymization**

**Research & Analytics:**

* **All analytics use de-identified data only**  
  * No personally identifiable information (PII)  
  * Aggregated metrics only  
  * Minimum cohort size: 100 users before showing any aggregate stat  
* **Community features use pseudonyms**  
  * User-chosen display names (not real names)  
  * No profile pictures in community areas  
  * Location shown only as city/state level (not exact)  
* **Aggregate insights never traceable to individuals**  
  * "60% of Vata-dominant users report sleep improvements" ✓  
  * Never: "User X improved their sleep" ✗  
* **Opt-out of anonymized data usage entirely**  
  * Complete opt-out available in settings  
  * No penalty for opting out  
  * Can change decision anytime

**Data Minimization:**

* Only collect data necessary for features user is using  
* Don't collect location if user doesn't want weather/seasonal features  
* Don't collect genetic data unless user uploads it  
* Regular audits to identify and delete unnecessary data

**Compliance**

**HIPAA Compliance (US Users):**

* **Business Associate Agreements** with all subprocessors  
* **HIPAA Security Rule compliance:**  
  * Administrative safeguards (access controls, training)  
  * Physical safeguards (secure data centers)  
  * Technical safeguards (encryption, audit controls)  
* **HIPAA Privacy Rule compliance:**  
  * Notice of Privacy Practices provided at signup  
  * User authorization for all uses beyond treatment/payment/operations  
  * Right to access, amend, and receive accounting of disclosures  
* **Breach notification protocols:**  
  * 60-day notification to affected users  
  * Notification to HHS for breaches affecting 500+ users  
  * Detailed incident reports

**GDPR Compliance (EU Users):**

* **Lawful basis for processing**: Consent (freely given, specific, informed, unambiguous)  
* **Data subject rights:**  
  * Right to access (download your data)  
  * Right to rectification (correct inaccurate data)  
  * Right to erasure ("right to be forgotten")  
  * Right to restrict processing  
  * Right to data portability  
  * Right to object  
  * Rights related to automated decision-making  
* **Data Protection Officer** appointed and contact info provided  
* **Privacy by design and by default**  
* **Data Processing Agreements** with all processors  
* **International data transfers**: Standard Contractual Clauses (SCCs)

**Other Regulations:**

* **CCPA/CPRA** (California): Consumer privacy rights respected  
* **State privacy laws**: Compliance with all applicable US state laws  
* **Medical device regulations**: Not classified as medical device (wellness tool only)  
* **FTC regulations**: Truthful advertising, no deceptive practices

**Regular Security Audits:**

* **Annual penetration testing** by third-party security firms  
* **Quarterly vulnerability assessments**  
* **SOC 2 Type II certification** (target within 18 months of launch)  
* **Regular code security reviews**  
* **Dependency vulnerability scanning** (automated)

**Breach Notification Protocols:**

* **Detection**: Automated monitoring for unusual access patterns  
* **Assessment**: Incident response team evaluates severity within 24 hours  
* **Containment**: Immediate action to limit breach scope  
* **Notification**:  
  * Users notified within 60 days (HIPAA) or 72 hours (GDPR)  
  * Clear explanation of what happened, what data affected, what we're doing  
  * Free credit monitoring if financial data compromised  
  * Regulatory notifications as required  
* **Remediation**: Fix vulnerabilities, prevent recurrence  
* **Post-incident review**: Learn and improve

**Data Retention Policies:**

* **Active accounts**: Data retained indefinitely while account active  
* **Inactive accounts**: After 2 years of inactivity, user notified and data archived  
* **Deleted accounts**: 30-day soft delete, then permanent deletion  
* **Backups**: Encrypted backups retained for 90 days, then securely deleted  
* **Audit logs**: Retained for 7 years (compliance requirement)  
* **User control**: Users can request earlier deletion anytime


---

# **Integrations** {#integrations}

**Wearable Devices**

**Apple Health**

* **Data Types**: Sleep analysis, steps, heart rate, HRV, respiratory rate, blood oxygen, body temperature, mindful minutes, nutrition (if logged), cycle tracking  
* **Integration Method**: HealthKit API  
* **Authentication**: OAuth 2.0 with user permission prompts  
* **Sync Frequency**: Real-time when app is open, background sync every 1 hour  
* **Data Flow**: Apple Health → AyuAware (read-only, AyuAware doesn't write back)

**Google Fit**

* **Data Types**: Same as Apple Health  
* **Integration Method**: Google Fit API  
* **Authentication**: OAuth 2.0  
* **Sync Frequency**: Real-time \+ hourly background  
* **Data Flow**: Google Fit → AyuAware (read-only)

**Oura Ring**

* **Data Types**: Sleep stages (deep, REM, light), HRV, body temperature variations, resting heart rate, respiratory rate, readiness score, activity score  
* **Integration Method**: Oura API v2  
* **Authentication**: OAuth 2.0  
* **Sync Frequency**: Automatic sync each morning after Oura processes overnight data  
* **Why Valuable**: Exceptionally accurate sleep and HRV data, temperature trends excellent for dosha tracking

**WHOOP**

* **Data Types**: Strain (daily exertion), recovery score, sleep performance, HRV, resting heart rate, respiratory rate, skin temperature  
* **Integration Method**: WHOOP API  
* **Authentication**: OAuth 2.0  
* **Sync Frequency**: Real-time \+ daily summaries  
* **Why Valuable**: Recovery metrics align with Ayurvedic concept of balancing activity and rest

**Fitbit**

* **Data Types**: Sleep, steps, heart rate, active minutes, floors climbed, calories burned  
* **Integration Method**: Fitbit Web API  
* **Authentication**: OAuth 2.0  
* **Sync Frequency**: Every 15 minutes when app active, hourly background  
* **Data Flow**: Fitbit → AyuAware (read-only)

**Garmin**

* **Data Types**: Comprehensive fitness metrics, sleep, stress score, body battery, VO2 max, training load  
* **Integration Method**: Garmin Health API  
* **Authentication**: OAuth 2.0  
* **Sync Frequency**: Real-time \+ hourly background  
* **Why Valuable**: Stress score and body battery align with energy/vitality tracking

**Integration Setup Process:**

1. User taps "Connect \[Device\]" in Profile → Privacy & Security → Connected Devices  
2. OAuth flow opens in secure browser  
3. User logs into wearable account  
4. Permission screen shows exactly what data AyuAware will access  
5. User approves  
6. Connection confirmed, initial data sync begins  
7. Ongoing automatic syncs in background

**Sync Status Visibility:**

* Last sync time shown for each device  
* "Syncing..." indicator when active  
* Error messages if sync fails (with troubleshooting steps)  
* Manual "Sync Now" button for immediate refresh

**Data Mapping to Ayurvedic Concepts:**

* **Sleep fragmentation** → Vata imbalance indicator  
* **HRV decline** → Stress, approaching imbalance, low Ojas  
* **Night awakenings 10pm-2am** → Pitta imbalance indicator  
* **Excessive sleep (\>9 hours)** → Kapha imbalance indicator  
* **Low recovery score** → Depletion, need for rest and nourishment  
* **High strain with poor recovery** → Risk of burnout, Pitta/Vata aggravation

**Health Apps**

**MyFitnessPal** (Optional)

* **Purpose**: Alternative to photo meal logging for users who prefer manual entry  
* **Data Types**: Meals, calories, macronutrients, micronutrients  
* **Integration Method**: MyFitnessPal API  
* **Authentication**: OAuth 2.0  
* **Sync**: Daily  
* **Ayurvedic Enhancement**: Digital Twin analyzes nutritional data through dosha lens, suggests adjustments

**Cronometer** (Optional)

* **Purpose**: Detailed micronutrient tracking  
* **Data Types**: Complete nutritional breakdown  
* **Why Valuable**: Identify deficiencies that align with dosha imbalances (e.g., low iron → Vata, B vitamin needs)  
* **Integration Method**: API  
* **Sync**: Daily

**Headspace / Calm** (Optional)

* **Purpose**: Meditation practice tracking  
* **Data Types**: Meditation sessions, duration, type  
* **Integration Method**: API (if available)  
* **Sync**: Daily  
* **Ayurvedic Context**: Meditation tracked as Sattva-building practice

**Strava**

* **Purpose**: Athletic activity tracking  
* **Data Types**: Runs, rides, swims with pace, distance, heart rate, perceived exertion  
* **Integration Method**: Strava API  
* **Authentication**: OAuth 2.0  
* **Sync**: After each activity  
* **Ayurvedic Analysis**: Activity intensity evaluated against constitution (is this too much for Vata? Perfect for Kapha?)

**Medical Records (V2 \- Future)**

**Epic MyChart**

* **Purpose**: Access lab results, medical history, medications, allergies  
* **Data Types**: Labs, diagnoses, medications, visit notes, immunizations  
* **Integration Method**: FHIR API (Fast Healthcare Interoperability Resources)  
* **Authentication**: Epic OAuth with patient consent  
* **Sync**: On-demand and weekly automated  
* **Ayurvedic Value**: Automatic lab result interpretation, medication interaction checking with herbs

**Cerner**

* **Purpose**: Hospital records access  
* **Data Types**: Similar to Epic  
* **Integration Method**: FHIR API  
* **Authentication**: OAuth

**CommonHealth**

* **Purpose**: Aggregated health records from multiple providers  
* **Data Types**: Comprehensive medical history  
* **Integration Method**: CommonHealth API  
* **Benefits**: Single integration point for multiple medical systems

**Smart on FHIR**

* **Purpose**: Universal medical data access  
* **Standard**: FHIR for interoperability  
* **Benefits**: Access records from any FHIR-compliant system  
* **Patient control**: User authorizes which records to share with AyuAware

**Privacy Note for Medical Integrations:**

* All medical data treated as HIPAA protected health information (PHI)  
* Encrypted at rest and in transit  
* Minimal necessary data principle  
* User can disconnect anytime  
* Medical data never used for marketing or sold to third parties

**Practitioner Tools (V2 \- Future)**

**SimplePractice**

* **Purpose**: Appointment scheduling, session notes, billing  
* **Integration Method**: SimplePractice API  
* **Features**:  
  * Sync appointments to AyuAware calendar  
  * Share protocols and health data with provider (user consent)  
  * Practitioner can add notes to user's AyuAware profile  
  * Billing integration (if practitioner uses AyuAware)

**Google Calendar**

* **Purpose**: Appointment sync, reminder integration  
* **Integration Method**: Google Calendar API  
* **Authentication**: OAuth 2.0  
* **Features**:  
  * Practitioner appointments appear in AyuAware  
  * Protocol reminders sync to Google Calendar  
  * Check-in reminders sync

**Zoom**

* **Purpose**: Telemedicine consultations  
* **Integration Method**: Zoom API  
* **Features**:  
  * One-click join for practitioner video appointments  
  * Automatic meeting links for scheduled consultations  
  * Recording storage (with consent)

**Secure Messaging (Custom or HIPAA-compliant platform)**

* **Purpose**: HIPAA-compliant communication with providers  
* **Features**:  
  * Encrypted messaging  
  * Share specific data points or protocol updates  
  * Request appointments or prescription refills  
  * Provider can send homework or recommendations  
* **Options**: Build custom or integrate with existing (e.g., OhMD, TigerConnect)

**Practice Better** (for Ayurvedic practitioners and nutritionists)

* **Purpose**: Client management, protocols, meal plans  
* **Integration Method**: API (if available)  
* **Features**: Practitioners using Practice Better can connect with clients using AyuAware

**Integration Management**

**User Controls (in Profile → Privacy & Security → Integrations):**

* List of all connected services  
* Last sync time for each  
* Data types being shared  
* \[Disconnect\] button for each  
* \[Reconnect\] if connection broken  
* \[Edit Permissions\] to change what data is shared

**Troubleshooting:**

* **Connection Failed**: Step-by-step troubleshooting guide  
* **Data Not Syncing**: Check app permissions, re-authenticate  
* **Sync Errors**: Clear explanation of issue, how to fix  
* **Support**: Link to help articles for each integration

**Future Integrations Roadmap:**

* **Glucose Monitors** (Continuous Glucose Monitors \- CGM): Dexcom, FreeStyle Libre  
* **Smart Scales**: Withings, QardioBase for body composition  
* **Menstrual Cycle Apps**: Flo, Clue for detailed cycle tracking  
* **Therapy Apps**: BetterHelp, Talkspace for mental health integration  
* **Pharmacy Apps**: For medication adherence tracking  
* **Smart Home**: Circadian lighting, temperature optimization for sleep

---

#                   **Authentication & Permissions** {#authentication-&-permissions}

**Registration**

**Sign-Up Flow:**

1. **Landing Page**  
   * "Get Started" button  
   * "Already have an account? Sign In" link  
2. **Registration Form**  
   * **Email**: Valid email format required, email verification sent  
   * **Full Name**: First and last name  
   * **Password**:  
     * Minimum 8 characters  
     * Must include: 1 uppercase, 1 lowercase, 1 number, 1 special character  
     * Strength meter shown (Weak/Medium/Strong)  
   * **Confirm Password**: Must match  
   * **Optional**: "Sign up with Google" or "Sign up with Apple" (OAuth)  
3. **Terms & Agreements**  
   * ☐ I agree to the Terms of Service (link)  
   * ☐ I agree to the Privacy Policy (link)  
   * ☐ I acknowledge the HIPAA Notice (link, US users only)  
   * ☐ (Optional) I agree to receive marketing emails and product updates  
   * All checkboxes must be checked except marketing  
4. **Email Verification**  
   * Verification email sent to provided address  
   * "Check your email for verification link"  
   * "Didn't receive? Resend verification email"  
   * User can't access app until email verified  
   * Verification link expires in 24 hours  
5. **Welcome & Onboarding**  
   * After verification, user logs in  
   * Immediately starts AI-guided onboarding flow (constitutional assessment, etc.)

**Alternative Sign-Up Methods:**

**Sign Up with Google:**

* OAuth 2.0 flow  
* Requests permissions: Email, Name, Profile Picture  
* Email automatically verified (Google confirms it)  
* Still must accept Terms/Privacy Policy/HIPAA

**Sign Up with Apple:**

* Sign in with Apple  
* Option to hide email (Apple provides relay email)  
* Email automatically verified  
* Still must accept Terms/Privacy Policy/HIPAA

**Password Requirements:**

* Minimum 8 characters (recommended 12+)  
* At least 1 uppercase letter (A-Z)  
* At least 1 lowercase letter (a-z)  
* At least 1 number (0-9)  
* At least 1 special character (\!@\#$%^&\*)  
* Cannot be common password (checked against known leaked password database)  
* Cannot be same as email or name

**Email Verification:**

* Required before account access  
* Verification email includes:  
  * Welcome message  
  * Verification link (24-hour expiration)  
  * What to expect next  
  * Support contact if issues  
* After verification: Redirect to login → Onboarding

**Login**

**Login Form:**

* **Email**: Email used at registration  
* **Password**: User's password  
* **Remember Me**: Optional checkbox (keeps user logged in for 30 days)  
* \[Forgot Password?\] link  
* \[Sign In\] button  
* "Don't have an account? Sign Up" link

**Alternative Login Methods:**

* \[Continue with Google\]  
* \[Continue with Apple\]  
* Must use same method as registration (if signed up with Google, must log in with Google)

**Forgot Password Flow:**

1. Click "Forgot Password?"  
2. Enter email address  
3. "Send Reset Link" button  
4. Password reset email sent (link expires in 1 hour)  
5. Click link in email  
6. Enter new password (must meet requirements)  
7. Confirm new password  
8. "Reset Password" button  
9. Password updated, redirect to login  
10. Log in with new password

**Two-Factor Authentication (2FA):**

* **Setup** (optional but recommended):  
  * In Profile → Privacy & Security → Enable 2FA  
  * Choose method: SMS or Authenticator App (Google Authenticator, Authy)  
  * For SMS: Enter phone number, receive verification code  
  * For Authenticator: Scan QR code, enter verification code  
  * Backup codes generated (10 single-use codes)  
  * Save backup codes securely  
* **Login with 2FA Enabled**:  
  * Enter email and password  
  * Prompted for 2FA code  
  * Enter code from SMS or authenticator app  
  * "Trust this device for 30 days" checkbox (optional)  
  * If code correct, logged in  
  * If code incorrect, can retry or use backup code  
* **Lost 2FA Access**:  
  * "Can't access your 2FA device?" link  
  * Enter backup code  
  * Or contact support with account verification

**Biometric Authentication** (Mobile App):

* **Face ID** (iPhone with Face ID)  
* **Touch ID** (iPhone/iPad with fingerprint sensor)  
* **Fingerprint** (Android devices)  
* **Setup**:  
  * After first login, prompted to enable biometric  
  * "Use Face ID to sign in?" / "Use Fingerprint?"  
  * Enable in settings anytime  
* **Usage**:  
  * Open app → Face ID / Fingerprint prompt  
  * Successful authentication → Access app  
  * Failed → Fall back to password login  
  * Every 30 days, password re-entry required (security measure)

**Session Management**

**Session Tokens:**

* **JWT (JSON Web Tokens)** for authentication  
* **Token Lifespan**: 7 days by default  
* **Refresh Tokens**: 30 days (allows silent re-authentication)  
* **Secure**: HttpOnly cookies (not accessible to JavaScript) \+ additional security headers

**Auto-Logout:**

* **Inactivity Timeout**: 30 minutes of no interaction (configurable in settings: 15/30/60/Never)  
* **Warning**: 2 minutes before timeout, show modal: "You'll be logged out in 2 minutes due to inactivity. Continue session?"  
* **Continue**: Resets timeout timer  
* **Ignore**: Automatically logged out after 2 minutes  
* **On Logout**: Return to login screen, session token invalidated

**Device Management:**

* **View Logged-In Devices**:  
  * Location: Profile → Privacy & Security → Active Sessions  
  * Each session shows:  
    * Device name (e.g., "iPhone 13 Pro")  
    * Browser (e.g., "Safari 17.0")  
    * Location (city, state based on IP)  
    * Last active timestamp  
    * "Current session" indicator  
  * \[Log Out\] button for each session  
  * \[Log Out All Other Devices\] button  
* **Remote Logout**:  
  * Immediately invalidates session token  
  * User on that device logged out next time they interact  
  * Useful if device lost or stolen

**Password Changes:**

* Changing password logs out all sessions except current  
* User must re-login on all other devices  
* Security measure to ensure unauthorized access ends

**Session Security:**

* **IP Address Tracking**: Unusual login locations trigger email alert  
* **Concurrent Session Limit**: Maximum 5 active sessions per account  
* **Session Hijacking Protection**:  
  * Token rotation on sensitive actions  
  * User agent and IP validation  
  * Encrypted tokens with short expiration

**Data Access Levels**

**User Roles within AyuAware:**

**Self (Standard User)**

**Full Access To:**

* Own complete health profile  
* All personal health data (wearables, labs, images, logs)  
* Conversation history with Digital Twin  
* All protocols (create, modify, activate, deactivate)  
* All projects  
* Learning content  
* Shop purchases  
* Personal settings and preferences

**Actions:**

* Create and modify protocols  
* Upload health data (images, labs, genetic data)  
* Connect wearable integrations  
* Share data with practitioners (explicit consent required)  
* Download/export own data  
* Delete own data or account

**Cannot:**

* Access other users' data  
* Access admin functions  
* Modify system settings or knowledge base

**Practitioner (With User Permission)**

**Access Only After User Explicitly Shares:**

**Shared Access Includes:**

* User's shared health data:  
  * Constitution (prakriti/vikriti)  
  * Health metrics selected by user  
  * Lab results (if user shares)  
  * Protocols and progress  
  * Specific conversations (if user shares)  
  * Symptom reports  
  * Images (tongue, etc. if user shares)

**Actions:**

* **View** shared health data (read-only on most data)  
* **Add notes** to user's profile (practitioner observations)  
* **Collaborate on protocols**:  
  * Comment on user's protocols  
  * Suggest modifications  
  * Create recommended protocols (user must approve)  
* **Message user** through secure HIPAA-compliant messaging  
* **Schedule appointments** (if calendar integration enabled)  
* **Request specific data**: "Can you share your recent lab work?"

**Cannot:**

* Modify user's data directly (except practitioner notes)  
* Access data user hasn't shared  
* Access other patients beyond their client list  
* See financial information (subscription, purchases)  
* Change user's preferences or settings  
* Delete user's data

**Practitioner Account Features:**

* **Client Dashboard**: See all clients who've shared access  
* **Client Overview**: Each client's progress, active protocols, recent data  
* **Communication Hub**: HIPAA-compliant messaging with clients  
* **Protocol Library**: Save custom protocols to reuse with multiple clients  
* **Notes System**: Private practitioner notes (not visible to client unless explicitly shared)

**Access Control:**

* **User grants access**: User invites practitioner by email or practitioner code  
* **Granular permissions**: User chooses exactly what to share:  
  * ☐ Constitution and current state  
  * ☐ Daily check-ins and symptom reports  
  * ☐ Wearable data (sleep, activity, HRV)  
  * ☐ Lab results  
  * ☐ Genetic data  
  * ☐ Images (scans)  
  * ☐ Meal logs  
  * ☐ Supplement logs  
  * ☐ Protocols and adherence data  
  * ☐ Conversation history with Digital Twin  
* **Time-limited access**: Optional expiration (e.g., 3 months, 6 months, 1 year, or indefinite)  
* **Revoke anytime**: User can revoke practitioner access instantly  
* **Audit log**: User can see what practitioner accessed and when

**Admin (AyuAware Team \- Minimal Access)**

**By Default, Admins Have NO Access To:**

* Individual user health data  
* User conversations  
* User images or scans  
* User personal information beyond email (for support)

**Admin Access Requires:**

* **User consent**: Explicit permission for each support case  
* **Logging**: All admin access logged with timestamp, reason, admin ID  
* **Justification**: Written reason required ("User reported bug with tongue analysis")  
* **Time-limited**: Access expires after issue resolved

**Admin Can Access (With User Consent):**

* Specific user profile for troubleshooting  
* Error logs related to user's issue  
* Specific data points causing technical issues  
* Conversation logs (if user reports AI behavior issue)

**Admin Functions (No User Data Involved):**

* **System Monitoring**: Server health, performance metrics, error rates  
* **Aggregate Analytics** (all de-identified):  
  * User growth metrics  
  * Feature usage statistics (e.g., "60% of users use tongue scanning")  
  * Protocol effectiveness rates (aggregated, not individual)  
  * Retention and engagement metrics  
* **Content Management**:  
  * Update Ayurvedic knowledge base  
  * Add new herbs to database  
  * Update educational content  
  * Manage shop products  
* **User Support**:  
  * Respond to support tickets  
  * Reset passwords (if user requests via verified email)  
  * Troubleshoot technical issues  
  * Resolve billing issues  
* **System Administration**:  
  * Deploy updates  
  * Manage infrastructure  
  * Security monitoring  
  * Backup management

**Admin Audit Trail:**

* Every admin action logged  
* Logs include: Admin ID, Action, Timestamp, Reason, User affected (if applicable)  
* Logs retained for 7 years (compliance requirement)  
* Logs reviewed quarterly for unauthorized access

**Principle of Least Privilege:**

* Admins only get access they need for specific job function  
* Support admins can't access infrastructure  
* Infrastructure admins can't access user data  
* Separation of duties enforced

**Custom Roles (Future \- Enterprise Feature)**

For wellness centers, retreat centers, or large practices:

**Roles Might Include:**

* **Receptionist**: Can schedule appointments, view basic contact info, cannot see health data  
* **Wellness Coach**: Can see protocols and adherence, can message clients, limited health data  
* **Senior Practitioner**: Full practitioner access plus can supervise junior practitioners  
* **Researcher**: Access to anonymized aggregate data for clinical studies

**Role Permissions Customizable:**

* Each organization can define roles  
* Assign specific permissions to each role  
* Users still control what data each role can see

---

#                 **Pricing** {#pricing}

**Pricing**

**Plans**

**Free Plan \- $0/month**

**Included:**

* Constitutional assessment (Prakriti quiz)  
* Basic chat with Digital Twin: **20 messages per month**  
* Daily check-ins (unlimited)  
* 1 active protocol at a time  
* Basic health data tracking:  
  * Manual entry for all metrics  
  * No wearable integrations  
  * Sleep, energy, mood, digestion logging  
* Educational content access (Learn section \- all lessons)  
* Community forums access (read-only)

**Limitations:**

* No wearable device integrations  
* No image analysis (tongue, meal, product scans)  
* No morning summaries or prediction alerts  
* No lab result analysis  
* No genetic data analysis  
* No protocol export  
* No practitioner collaboration  
* Email support only (48-hour response time)

**Best For:**

* Users exploring Ayurveda  
* Those who want to try AyuAware before committing  
* Users comfortable with manual data entry  
* Budget-conscious individuals

**Personal Plan \- $9.99/month** (or $95.88/year \- save 20%)

**Everything in Free, Plus:**

* **Unlimited chat** with Digital Twin  
* **Up to 3 active protocols** simultaneously  
* **Wearable integrations** (unlimited devices):  
  * Apple Health, Google Fit, Fitbit, Oura, WHOOP, Garmin  
  * Automatic data sync  
  * Ayurvedic interpretation of all metrics  
* **Image analysis**: **10 scans per month**  
  * Tongue analysis  
  * Meal analysis  
  * Product scanning  
  * Skin analysis  
* **Morning summaries** and **prediction alerts**  
  * Personalized daily forecasts  
  * Proactive imbalance warnings  
  * Environmental/seasonal context  
* **Advanced health data visualizations**:  
  * Trend graphs (7-day, 30-day, 90-day, 1-year views)  
  * Pattern recognition across data types  
  * Correlation insights  
* **Protocol library** access (save favorite protocols, browse community protocols)  
* **Email support** with 24-hour response time

**Limitations:**

* Limited scans (10/month \- additional scans available as add-on)  
* No lab result analysis  
* No genetic analysis  
* No practitioner collaboration features  
* No priority support

**Best For:**

* Committed Ayurveda practitioners  
* Users with wearable devices  
* Those wanting personalized daily guidance  
* People working on 1-2 health goals simultaneously

**Premium Plan \- $24.99/month** (or $239.88/year \- save 20%)

**Everything in Personal, Plus:**

* **Unlimited image analysis**  
  * Scan as many tongues, meals, products as you want  
  * No monthly limits  
* **Lab result analysis**: **3 uploads per month**  
  * Blood work interpretation (CBC, metabolic panel, lipids, hormones, etc.)  
  * Ayurvedic translation of biomarkers  
  * Root cause analysis  
  * Comprehensive protocol generation from labs  
* **Genetic data analysis** (one-time upload):  
  * 23andMe, Ancestry DNA, or other raw data  
  * Constitutional validation through genetics  
  * Personalized recommendations based on genetic variants  
  * Lifetime access to genetic insights  
* **Practitioner collaboration portal**:  
  * Share data with unlimited practitioners  
  * HIPAA-compliant secure messaging  
  * Collaborative protocol development  
  * Granular permission controls  
  * Provider dashboard for practitioners  
* **Priority support**:  
  * Live chat support  
  * Email with 12-hour response time  
  * Priority bug fixes  
  * Direct access to support team  
* **Export protocols and health reports**:  
  * PDF exports for sharing with providers  
  * Comprehensive health summaries  
  * Protocol documentation  
* **Early access to new features**:  
  * Beta features before general release  
  * Influence product roadmap with feedback  
  * Exclusive webinars and Q\&As

**Best For:**

* Power users managing multiple health goals  
* Those working with Ayurvedic practitioners or doctors  
* Users with complex health situations  
* People wanting deepest personalization (genetics \+ labs)  
* Serious health optimization enthusiasts

**Practitioner Plan \- $99/month** (or $950/year \- save 20%)

**For Ayurvedic Practitioners, Nutritionists, Wellness Coaches:**

**Includes:**

* **Manage up to 20 client accounts**  
  * Each client gets Personal plan features  
  * Centralized client dashboard  
  * Client progress tracking  
* **Collaborative protocol development**:  
  * Create protocols for clients  
  * Comment and modify client protocols  
  * Track client adherence  
  * Outcome tracking across clients  
* **Client data access** (with permission):  
  * View all shared health data  
  * Add practitioner notes (private or shared)  
  * Request specific data from clients  
* **Appointment scheduling integration**:  
  * Sync with Google Calendar, SimplePractice  
  * Automated reminders for clients  
  * Video consultation integration (Zoom)  
* **HIPAA-compliant messaging**:  
  * Secure communication with all clients  
  * Message templates for common scenarios  
  * File sharing (protocols, meal plans, education)  
* **Practice management tools**:  
  * Client intake forms  
  * Session notes templates  
  * Billing integration (optional)  
  * Referral tracking  
* **Protocol library**:  
  * Save custom protocols  
  * Reuse protocols across clients  
  * Share protocols with other practitioners (optional)  
* **Custom branding option**:  
  * Add your logo to protocols  
  * Customize color scheme  
  * "Powered by AyuAware" in footer  
* **Analytics dashboard**:  
  * Client outcomes aggregated  
  * Protocol effectiveness rates  
  * Client engagement metrics  
* **Continuing education**:  
  * Advanced practitioner training modules  
  * Case study library  
  * Peer consultation forums  
* **Priority support**:  
  * Dedicated practitioner support team  
  * Training and onboarding assistance  
  * Technical support for clients

**Additional Clients:**

* $4/month per additional client beyond 20

**White-Label Option Available:**

* Completely remove AyuAware branding  
* Custom domain (yourpractice.ayuaware.com or your own domain)  
* Custom welcome flows  
* \+$50/month for white-label

**Best For:**

* Ayurvedic practitioners and consultants  
* Nutritionists with Ayurvedic focus  
* Yoga teachers offering wellness guidance  
* Health coaches using Ayurvedic principles  
* Wellness centers with multiple practitioners

**Enterprise Plan \- Custom Pricing**

**For Wellness Centers, Yoga Studios, Retreat Centers, Large Practices:**

**Everything in Practitioner Plan, Plus:**

* **Unlimited practitioner accounts**  
* **Unlimited client accounts**  
* **Custom integrations**:  
  * Integrate with your practice management software  
  * Custom data imports/exports  
  * API access for advanced use cases  
* **White-label full application**:  
  * Your branding throughout  
  * Custom domain  
  * No AyuAware branding anywhere  
  * Custom welcome and onboarding flows  
* **Dedicated account management**:  
  * Assigned customer success manager  
  * Quarterly business reviews  
  * Strategic planning support  
* **Custom feature development**:  
  * Build features specific to your needs  
  * Priority feature requests  
  * Dedicated development resources (depending on scope)  
* **Training and onboarding**:  
  * On-site or virtual training for all staff  
  * Train-the-trainer programs  
  * Ongoing education and certification  
  * Custom training materials  
* **Advanced analytics**:  
  * Custom reporting dashboards  
  * Aggregate client outcomes for research  
  * Export data for publications  
* **API access**:  
  * Programmatic access to AyuAware  
  * Build custom integrations  
  * Embed AyuAware in your own apps  
* **SLA (Service Level Agreement)**:  
  * 99.9% uptime guarantee  
  * Priority incident response  
  * Dedicated support team  
* **Data residency options**:  
  * Choose where your data is stored  
  * Dedicated database instance  
  * Enhanced compliance support

**Pricing:**

* Custom based on:  
  * Number of practitioners  
  * Number of clients  
  * Custom features required  
  * Support level needed  
  * Integration complexity  
* **Starting at $500/month**  
* Annual contracts with quarterly payments

**Best For:**

* Wellness centers with 5+ practitioners  
* Yoga studios offering wellness programs  
* Ayurvedic retreat centers  
* Multi-practitioner clinics  
* Research institutions  
* Corporate wellness programs

**Usage-Based Add-Ons**

**For Users Exceeding Plan Limits:**

**AI Credits** (Personal Plan users who exceed 20 messages on Free tier before upgrading):

* **$5 for 50 additional messages**  
* Auto-purchase option (charges when limit reached)  
* Messages reset monthly

**Image Analysis Packs** (Personal Plan users who exceed 10 scans/month):

* **$5 for 10 additional scans**  
* No expiration (use anytime)  
* Bundle discounts:  
  * 25 scans for $10 (60% discount)  
  * 50 scans for $18 (64% discount)

**Lab Analysis** (Premium Plan users who exceed 3 uploads/month):

* **$10 for 1 additional lab analysis**  
* Comprehensive interpretation included  
* Bundle: 5 additional analyses for $40 (20% discount)

**Storage** (All paid plans include 5 GB):

* **$2/month per additional GB**  
* Needed if extensive photo history (years of daily tongue photos, meal logs)  
* Monitor usage in Profile → Data & Exports

**Practitioner Connections** (Premium Plan includes unlimited, but listed for transparency):

* Included in Premium  
* Not sold as add-on (upgrade to Premium if needed)

**Video Consultations with AyuAware Practitioners** (Future):

* **$75 for 30-minute consultation**  
* **$120 for 60-minute consultation**  
* With verified, AyuAware-trained Ayurvedic practitioners  
* Not required for app usage (optional service)

**Annual Billing (20% Discount)**

**Personal Plan:**

* Monthly: $9.99/month \= $119.88/year  
* Annual: **$95.88/year** (saves $24 \= 20%)  
* **$7.99/month effective rate**

**Premium Plan:**

* Monthly: $24.99/month \= $299.88/year  
* Annual: **$239.88/year** (saves $60 \= 20%)  
* **$19.99/month effective rate**

**Practitioner Plan:**

* Monthly: $99/month \= $1,188/year  
* Annual: **$950/year** (saves $238 \= 20%)  
* **$79.17/month effective rate**

**Annual Benefits:**

* 20% cost savings  
* Lock in current pricing (protected from price increases)  
* Uninterrupted service (no monthly renewal hassles)  
* One-time annual receipt for taxes/reimbursement

**Refund Policy for Annual:**

* **30-day money-back guarantee**  
* Cancel within 30 days of annual purchase → full refund  
* After 30 days → prorated refund for unused months  
* Example: Cancel after 5 months → refund for remaining 7 months

**Payment Methods**

**Accepted Payment Methods:**

* **Credit/Debit Cards**: Visa, Mastercard, American Express, Discover  
* **PayPal**: Link PayPal account for automatic payments  
* **Apple Pay**: iOS users can pay with Apple Pay  
* **Google Pay**: Android users can pay with Google Pay  
* **ACH/Bank Transfer**: Enterprise plans only, invoice billing

**Payment Processing:**

* **Stripe**: All card payments processed through Stripe (PCI-DSS compliant)  
* **Automatic Renewal**: Subscriptions renew automatically  
* **Billing Date**: Date of initial subscription (e.g., subscribed Jan 15 → billed 15th each month)  
* **Failed Payment**: Email notification, 3 retry attempts over 10 days, then account downgraded to Free

**Invoices:**

* **Email Receipts**: Sent immediately after each charge  
* **Invoice History**: Available in Profile → Subscription & Billing  
* **Download Invoices**: PDF format for accounting/reimbursement  
* **Tax**: Sales tax applied based on location (if applicable)

**Enterprise Invoicing:**

* Invoice sent 14 days before payment due  
* Net-30 payment terms  
* Purchase order (PO) numbers supported  
* Wire transfer option available

**Free Trial**

**Premium Plan Free Trial:**

* **14-day free trial** for Premium Plan  
* Full Premium features included  
* No credit card required to start trial  
* After 14 days:  
  * Prompted to add payment method  
  * Can downgrade to Personal or Free  
  * Or upgrade to Premium with payment  
* Trial only available once per user

**Trial Features:**

* Unlimited image analysis  
* Lab result analysis (3 uploads during trial)  
* Genetic analysis  
* Practitioner collaboration  
* Full experience of Premium

**Trial Purpose:**

* Let users experience full power before committing  
* Especially valuable for testing genetic/lab analysis  
* See if practitioner collaboration works for their needs

**Plan Changes**

**Upgrading:**

* **Immediate Effect**: New features available instantly  
* **Prorated Billing**: Credit for unused portion of current plan applied to new plan  
* Example: Upgrade from Personal ($9.99) to Premium ($24.99) on day 15 of month  
  * Credit: \~$5 (half of $9.99)  
  * Charge: $24.99 \- $5 \= $19.99 for first month of Premium  
  * Subsequent months: Full $24.99

**Downgrading:**

* **Effect**: Changes at end of current billing cycle  
* **Reason**: You've already paid for current month's features  
* **Data Retention**: All data kept, just limited features  
* Example: Downgrade Premium → Personal on Jan 20  
  * Premium features until Feb 1 (end of billing cycle)  
  * Feb 1: Switches to Personal, billed $9.99

**Canceling:**

* **Effect**: Cancel anytime, access until end of billing period  
* **Automatic Downgrade**: Account becomes Free after cancellation date  
* **Data**: All data retained (can reactivate anytime)  
* **Reactivation**: Re-subscribe anytime, pick up where you left off

**Pausing Subscription** (Future Feature):

* Pause for 1-3 months (travel, financial hardship)  
* Data retained  
* Don't get billed during pause  
* Resume anytime

**Refund Policy**

**General Refund Policy:**

* **14-day money-back guarantee** on all new subscriptions  
* Cancel within 14 days of first charge → full refund  
* After 14 days → cancel anytime, access until end of billing period, no refund for partial month

**Annual Subscriptions:**

* **30-day money-back guarantee** for annual plans  
* Cancel within 30 days → full refund  
* After 30 days → prorated refund for unused months

**Extenuating Circumstances:**

* Medical emergencies, financial hardship  
* Contact support for consideration on case-by-case basis  
* May offer partial refunds or credits

**Add-On Purchases:**

* **Non-refundable** once purchased (AI credits, scan packs, lab analyses)  
* Reason: Digital goods immediately accessible  
* Exception: Technical issues preventing use (full refund)

**Non-Profit & Student Discounts**

**Student Discount:**

* **50% off Personal Plan**: $4.99/month (instead of $9.99)  
* **Verification**: Valid .edu email address or student ID upload  
* **Eligibility**: Undergraduate, graduate, or continuing education students  
* **Duration**: Discount valid while student status confirmed (annual re-verification)

**Non-Profit / Wellness Organization Discount:**

* **30% off Practitioner Plan**: $69/month (instead of $99)  
* **Verification**: 501(c)(3) documentation or equivalent  
* **Eligibility**: Registered non-profits providing Ayurvedic/wellness services  
* **Contact**: Email partnerships@ayuaware.com to apply

**Low-Income/Hardship Program** (Future):

* Income-based sliding scale  
* Apply through support with income verification  
* Grants and scholarships for Premium access

**Referral Program (Future)**

**Refer a Friend:**

* **Your Reward**: $10 credit toward subscription  
* **Friend's Reward**: $10 off first month of paid plan  
* **How It Works**:  
  1. Share your unique referral link (found in Profile)  
  2. Friend signs up using your link  
  3. Friend subscribes to paid plan  
  4. You both get $10 credit  
* **Unlimited Referrals**: No cap on how many friends you can refer  
* **Tracking**: Dashboard shows referrals sent, signed up, credited

**Practitioner Referral Program:**

* **Refer Practitioners**: $50 credit for each practitioner who subscribes to Practitioner Plan  
* **Refer Clients**: Practitioners get free month for every 5 client referrals who subscribe

---

#        **Error Handling** {#error-handling}

**User-Facing Errors**

**Connection Issues:**

**No Internet Connection:**

* **Detection**: App detects no network connectivity  
* **Message**:

  📡 No Internet Connection  
    
  Looks like you're offline. AyuAware needs an internet connection to sync your data and chat with your Digital Twin.  
    
  What you can do:  
  • View cached health data  
  • Review past protocols  
  • Browse downloaded lessons  
    
  We'll sync automatically when you're back online.

* **Actions**:  
  * \[Retry\] button to check connection again  
  * Offline mode activates:  
    * Show cached data (read-only)  
    * Queue user actions (check-ins, logs) for sync when online  
    * Gray out features requiring internet (chat, scan, sync)  
* **Recovery**: When internet returns, auto-sync queued data, show toast "Back online\! Syncing your data..."

**Slow or Unstable Connection:**

* **Detection**: Request timeout or very slow response  
* **Message**:

  🐌 Slow Connection Detected  
    
  Your connection seems slow. This might take a moment...  
    
  \[Cancel\] \[Keep Waiting\]

* **Actions**:  
  * Show loading spinner with progress indicator  
  * Timeout after 30 seconds  
  * Retry with exponential backoff (1s, 2s, 4s, 8s, 16s)  
  * After 3 failed retries: Suggest checking connection and trying again later

**Server/API Issues:**

* **Detection**: 500-level HTTP errors, API unavailable  
* **Message**:

  😴 AyuAware is Taking a Brief Rest  
    
  We're experiencing a temporary issue on our end. This usually resolves in a few minutes.  
    
  Please try again shortly.  
    
  \[Try Again\]

* **Actions**:  
  * Automatic retry after 10 seconds (silent, in background)  
  * If persists, show "Report Issue" button  
  * Status page link: "Check System Status"  
  * Log error for engineering team

**AI Service Unavailable:**

**Digital Twin Temporarily Down:**

* **Detection**: Claude API returns error or timeout  
* **Message**:

  🧘 Your Digital Twin is Meditating  
    
  We're having trouble connecting to your Digital Twin right now. This is temporary.  
    
  While you wait, you can:  
  • View your health data  
  • Review your protocols  
  • Log check-ins  
  • Browse the Learn section  
    
  \[Try Again\] \[View Data\]

* **Fallback Behavior**:  
  * For simple queries: Use cached common responses  
    * "What are the three doshas?" → Serve from FAQ cache  
  * For complex queries requiring AI:  
    * Queue request, notify user when response ready  
    * Or suggest exploring Learn section for topic  
* **Recovery**: Retry AI connection every 30 seconds in background, notify user when back

**AI Response Timeout:**

* **Detection**: No response from AI within 60 seconds  
* **Message**:

  ⏱️ This is Taking Longer Than Usual  
    
  Your Digital Twin is thinking deeply about this...  
    
  \[Keep Waiting\] \[Cancel\]

* **Actions**:  
  * Extended timeout to 90 seconds  
  * If still no response: Cancel request, apologize, ask user to try again  
  * Log for engineering (may indicate complex query or system issue)

**AI Response Quality Issue:**

* **Detection**: Response seems malformed, empty, or nonsensical  
* **Message**:

  😅 Something Went Wrong  
    
  I didn't quite get that right. Let me try again.  
    
  \[Retry\] \[Report Issue\]

* **Actions**:  
  * Automatic retry with same query (different AI instance)  
  * If retry succeeds: Show response, no mention of error  
  * If retry fails: Apologize, ask user to rephrase or try different query  
  * Log response for quality review

**Image Analysis Failed:**

**Blurry or Low-Quality Image:**

* **Detection**: AI vision can't discern features clearly  
* **Message**:

  📸 Image Quality Too Low  
    
  I can't analyze this image clearly. For best results:  
    
  ✓ Good lighting (natural light is best)  
  ✓ Steady camera (avoid blur)  
  ✓ Close-up view (fill frame with tongue/meal)  
  ✓ Focus on subject  
    
  \[Retake Photo\] \[Upload Different Image\] \[Skip\]

* **Guidance**:  
  * Show example of good vs. bad photo  
  * Photo tips overlay for specific scan type  
  * Option to proceed anyway (lower confidence analysis)

**Wrong Type of Image:**

* **Detection**: Expected tongue photo, got meal photo (or vice versa)  
* **Message**:

  🤔 Unexpected Image Type  
    
  This looks like a \[meal/face/other\], but I was expecting a \[tongue\] photo.  
    
  Did you mean to:  
  • \[Analyze this as a meal\] (if meal detected)  
  • \[Upload a different image\]

* **Smart Routing**: If possible, analyze as detected type instead

**Image Processing Error:**

* **Detection**: Technical error in image processing pipeline  
* **Message**:

  ⚠️ Image Processing Error  
    
  We had trouble processing this image. Please try again.  
    
  If this keeps happening, try:  
  • Taking a new photo with better lighting  
  • Uploading a different image format (JPG or PNG)  
  • Checking your internet connection  
    
  \[Try Again\] \[Upload Different\] \[Contact Support\]

* **Actions**:  
  * Log error with image metadata (not image itself for privacy)  
  * Engineering team notified if error rate spikes  
  * Offer alternative: "Describe what you see and I can help without the image"

**Image Too Large:**

* **Detection**: File size exceeds limit (10 MB)  
* **Message**:

  📦 Image File Too Large  
    
  Maximum file size is 10 MB. Your image is \[X\] MB.  
    
  Try:  
  • Taking photo directly in app (auto-compressed)  
  • Reducing image resolution  
  • Using a different photo  
    
  \[Retake in App\] \[Choose Smaller Image\]

* **Auto-Compression**: If slightly over (10-15 MB), automatically compress and notify user

**Data Sync Issues:**

**Wearable Sync Failed:**

* **Detection**: OAuth connection broken, API returns error, no recent data  
* **Message**:

  ⌚ \[Oura/Fitbit/Apple Health\] Sync Issue  
    
  We're having trouble syncing your \[device\] data. Last successful sync: \[timestamp\].  
    
  This is usually fixed by:  
  1\. Opening the \[device app\] to ensure data is uploaded  
  2\. Checking that AyuAware still has permission in \[device app\] settings  
  3\. Disconnecting and reconnecting in AyuAware Settings  
    
  \[Reconnect Device\] \[View Troubleshooting Guide\] \[Dismiss\]

* **Troubleshooting Flow**:  
  * Check if OAuth token expired → Auto-refresh if possible  
  * Check if user revoked permissions → Prompt to re-authorize  
  * Check if device API is down → Show status, retry later  
  * Offer manual data entry alternative

**Lab Upload Processing Delay:**

* **Detection**: OCR/parsing takes longer than expected  
* **Message**:

  🔬 Analyzing Your Lab Results  
    
  Complex lab reports can take 2-3 minutes to process. I'm extracting all biomarkers and preparing your Ayurvedic analysis.  
    
  You'll get a notification when it's ready. Feel free to close this and come back\!  
    
  \[View Status\] \[Notify Me\]

* **Background Processing**: Queue job, send push notification when complete  
* **Estimated Time**: Show progress: "Processing... (\~60% complete)"

**Lab Upload Failed to Parse:**

* **Detection**: OCR can't extract data, unusual format  
* **Message**:

  📄 Couldn't Read This Lab Report  
    
  I had trouble reading this format. Lab reports vary a lot\!  
    
  Can you help?  
  • Try uploading a clearer scan/photo  
  • Make sure all text is visible  
  • If you have a different format (PDF vs. image), try that  
  • Or manually enter key results (I can guide you)  
    
  \[Upload Different File\] \[Manual Entry\] \[Contact Support\]

* **Fallback**: Offer to walk through manual data entry  
* **Support Escalation**: Flag for review \- engineering may add support for this format

**Invalid Input:**

**Form Validation Errors:**

* **Detection**: User enters invalid data in form fields  
* **Inline Validation**: Show error immediately when field loses focus

**Examples:**

Invalid Email:

Email: \[john@invalid\]  
❌ Please enter a valid email address  
Password Too Weak:

Password: \[abc123\]  
❌ Password must be at least 8 characters and include uppercase, lowercase, number, and special character  
Password strength: ████░░░░░░ Weak  
Invalid Date:

Date of Birth: \[13/45/1990\]  
❌ Please enter a valid date (MM/DD/YYYY)  
**Submit Button Disabled**: Until all validation passes

* Button grayed out with tooltip: "Please fix errors above"  
* When valid: Button enabled

**Helpful Inline Hints:**

* Show examples: "e.g., john@example.com"  
* Character counter for fields with limits  
* Show password requirements as checkmarks:

  ✓ At least 8 characters  
  ✓ Uppercase letter  
  ✗ Lowercase letter  
  ✗ Number  
  ✗ Special character  
**Out-of-Range Values:**

* **Energy Level (1-10)**: If user somehow enters 15

  ⚠️ Please enter a value between 1 and 10

* **Sleep Hours**: If user enters 25 hours

  ⚠️ That doesn't seem right. Please enter hours of sleep (0-24)

* Auto-correct if obvious typo (12.5 hours → valid, 125 hours → error)

**Rate Limiting / Usage Limits:**

**Free Plan Message Limit Reached:**

* **Detection**: User has sent 20 messages this month  
* **Message**:

  💬 Monthly Message Limit Reached  
    
  You've used all 20 free messages this month\! Your limit resets on \[date\].  
    
  Want to keep chatting?  
    
  \[Upgrade to Personal\] ($9.99/month \- unlimited)  
  \[Buy More Messages\] ($5 for 50 messages)  
  \[Wait Until Reset\] (\[X\] days)

* **Upgrade Path**: Seamless upgrade flow in app  
* **Grace Period**: Allow 1-2 extra messages to finish current conversation gracefully

**Personal Plan Scan Limit Reached:**

* **Detection**: User has used 10 scans this month  
* **Message**:

  📸 Monthly Scan Limit Reached  
    
  You've used all 10 image scans this month\! Limit resets on \[date\].  
    
  Options:  
    
  \[Upgrade to Premium\] ($24.99/month \- unlimited scans)  
  \[Buy Scan Pack\] ($5 for 10 scans)  
  \[Describe Instead\] (I can help without the image)  
  \[Wait for Reset\] (\[X\] days)

* **Alternative**: Offer text-based analysis (user describes what they see)

**Premium Plan Lab Upload Limit:**

* **Detection**: User uploading 4th lab this month (limit is 3\)  
* **Message**:

  🔬 Monthly Lab Analysis Limit  
    
  You've analyzed 3 lab reports this month (your plan's limit).  
    
  Need to analyze this one?  
    
  \[Purchase Additional Analysis\] ($10)  
  \[Save for Next Month\] (Resets \[date\])  
  \[Contact Support\] (if you need ongoing lab tracking)

* **Suggest**: If regularly exceeding, contact support for custom plan

**Admin-Facing Errors**

**Tool Execution Failure:**

**Detailed Error Log Entry:**

json  
{  
  "error\_id": "ERR-2024-01-15-0847",  
  "timestamp": "2024-01-15T08:47:23Z",  
  "tool\_name": "tongue\_analysis",  
  "action\_failed": "ai\_generate\_interpretation",  
  "user\_id": "user\_abc123\_hash",  
  "input\_data": {  
    "image\_url": "s3://ayuaware/uploads/abc123\_hash.jpg",  
    "image\_size": "2.4 MB",  
    "format": "JPEG"  
  },  
  "expected\_output": {  
    "coating\_analysis": "object",  
    "color\_analysis": "object",  
    "recommendations": "array"  
  },  
  "actual\_output": null,  
  "error\_message": "Claude API timeout after 60 seconds",  
  "stack\_trace": "\[detailed stack trace\]",  
  "retry\_attempts": 3,  
  "user\_notified": true,  
  "notification\_message": "Image analysis failed. Try retaking photo.",  
  "severity": "medium",  
  "impact": "Single user affected, feature degraded",  
  "alert\_sent": false  
}  
\`\`\`  
\*\*Alert Conditions:\*\*  
\- \*\*Critical\*\*: \>10% error rate on any tool for \>5 minutes → Page on-call engineer  
\- \*\*High\*\*: \>5% error rate for \>15 minutes → Slack alert to team  
\- \*\*Medium\*\*: Single recurring error pattern (same error 5\+ times) → Log for review  
\- \*\*Low\*\*: Isolated errors → Log only, review in weekly roundup  
\*\*Fallback Behavior:\*\*  
\- \*\*Tongue Analysis Fails\*\*: Offer manual symptom check-in, suggest trying again later  
\- \*\*Protocol Generation Fails\*\*: Offer pre-built protocol templates, retry with simpler prompts  
\- \*\*Morning Summary Fails\*\*: Send notification when ready (process in background)  
\*\*Auto-Remediation:\*\*  
\- \*\*Retry Logic\*\*: Automatic retry with exponential backoff (1s, 2s, 4s, 8s)  
\- \*\*Fallback to Simpler Model\*\*: If Claude Sonnet fails, try Haiku for less critical tasks  
\- \*\*Circuit Breaker\*\*: After 50% error rate, pause that tool for 5 minutes, use fallback  
\---  
\*\*Data Integration Issues:\*\*  
\*\*Wearable API Down:\*\*  
\- \*\*Detection\*\*: Oura/Fitbit/Apple Health API returns 500 errors  
\- \*\*Admin Alert\*\*:   
\`\`\`  
  ⚠️ Oura API Outage Detected  
    
  Status: DOWN  
  Affected Users: \~1,234 (estimated)  
  Duration: 23 minutes  
  Error Rate: 98%  
    
  Actions:  
  • Monitor Oura status page  
  • Notify users if outage extends \>2 hours  
  • Queue retries for when service resumes  
    
  \[View Details\] \[Notify Users\] \[Disable Integration Temporarily\]

* **User Communication**:  
  * If \>2 hours: In-app banner "We're aware of an issue with Oura syncing. This is on Oura's side. Your data will sync automatically when resolved."  
  * Email if \>24 hours

**OAuth Token Expired:**

* **Detection**: 401 Unauthorized from wearable API  
* **Admin Log**: "OAuth token expired for user \[hash\]. Attempted auto-refresh: \[success/failed\]"  
* **Auto-Remediation**:  
  * Try to refresh token using refresh token  
  * If success: Silent fix, no user notification  
  * If fails: Notify user to reconnect device

**Data Quality Issues:**

* **Detection**: Impossible values (sleep \= 48 hours, heart rate \= 300 bpm)  
* **Admin Alert**: "Data quality anomaly detected. Review user data for potential API bug or user error."  
* **Action**:  
  * Flag data point as "questionable"  
  * Don't use for analysis until verified  
  * Contact user if pattern continues: "We noticed unusual data from your \[device\]. Is your device working correctly?"

**Safety Boundary Violations:**

**Emergency Detection Triggered:**

* **Log Entry**:

json  
  {  
    "incident\_id": "SAFETY-2024-01-15-0912",  
    "timestamp": "2024-01-15T09:12:45Z",  
    "user\_id": "user\_xyz789\_hash",  
    "trigger": "emergency\_keywords\_detected",  
    "keywords": \["chest pain", "can't breathe"\],  
    "user\_message": "\[REDACTED for privacy\]",  
    "ai\_response": "Emergency protocol: Recommend 911",  
    "response\_time": "0.3 seconds",  
    "user\_action\_taken": "unknown",  
    "follow\_up\_needed": true,  
    "severity": "critical"  
  }  
\`\`\`  
\- \*\*Immediate Actions\*\*:  
  \- Emergency response delivered to user (\<1 second)  
  \- Incident logged for safety team review  
  \- If user continues conversation without seeking help, gentle reminder in next message  
  \- NO automatic 911 call (user privacy, could be hypothetical question)  
    
\- \*\*Follow-Up\*\*: Safety team reviews within 24 hours, looks for patterns, refines detection  
\*\*Medical Boundary Tested:\*\*  
\- \*\*Log\*\*: User asks Digital Twin to diagnose disease or prescribe medication  
\- \*\*Example\*\*:  
\`\`\`  
  User: "Do I have diabetes?"  
  AI Response: "I can't diagnose diabetes \- that requires medical testing. Your symptoms \[if mentioned\] could have many causes. Please see a doctor for proper diagnosis and testing. I'm happy to discuss Ayurvedic lifestyle support for blood sugar balance in general."  
\`\`\`  
\- \*\*Quality Check\*\*: Weekly review of boundary situations, ensure AI responding appropriately  
\- \*\*Improvement\*\*: If AI fails to catch medical question, add to training examples  
\*\*Inappropriate Content:\*\*  
\- \*\*Detection\*\*: User sends abusive, hateful, or sexually explicit messages  
\- \*\*Action\*\*:  
  \- AI responds: "I'm here to help with your health journey. Let's keep our conversation respectful and focused on wellness."  
  \- If persists: Temporary account suspension, review by trust & safety team  
  \- Log incident (user warned/suspended, reason, timestamp)  
\---  
\*\*Performance Degradation:\*\*  
\*\*Response Time Monitoring:\*\*  
\- \*\*Metrics Tracked\*\*:  
  \- Average AI response time (target: \<3 seconds)  
  \- 95th percentile response time (target: \<8 seconds)  
  \- Image analysis time (target: \<10 seconds)  
  \- Protocol generation time (target: \<15 seconds)  
  \- Page load time (target: \<2 seconds)  
\*\*Alert Thresholds:\*\*  
\- \*\*Yellow\*\*: Average response time \>5 seconds for \>5 minutes  
  \- Action: Monitor, identify cause  
\- \*\*Orange\*\*: Average response time \>8 seconds for \>5 minutes  
  \- Action: Scale up infrastructure, investigate bottlenecks  
\- \*\*Red\*\*: Average response time \>15 seconds or \>50% errors  
  \- Action: Page on-call, emergency scaling, consider disabling feature temporarily  
\*\*Auto-Scaling:\*\*  
\- Cloud infrastructure automatically scales based on load  
\- Trigger scaling at 70% capacity  
\- Monitor after scaling to ensure resolution  
\*\*Performance Optimization:\*\*  
\- \*\*Caching\*\*: Frequently asked questions cached (60\-second TTL)  
\- \*\*CDN\*\*: Static assets (images, CSS, JS) served from CDN  
\- \*\*Database Optimization\*\*: Regular query performance reviews  
\- \*\*AI Response Streaming\*\*: Stream AI responses (show partial response while generating)  
\---  
\#\#\# Graceful Degradation  
\*\*Limited AI Availability:\*\*  
\*\*Priority Queue System:\*\*  
When AI service is limited (high load, partial outage):  
1. \*\*Critical Functions\*\* (Always prioritized):  
   \- Emergency detection and safety responses  
   \- Boundary checking (medical scope limits)  
   \- Simple greetings and acknowledgments  
     
2. \*\*High Priority\*\*:  
   \- Daily check-ins (quick analysis)  
   \- Symptom tracking  
   \- Active protocol guidance  
     
3. \*\*Medium Priority\*\*:  
   \- General health questions  
   \- Educational responses  
   \- Image analysis  
     
4. \*\*Low Priority\*\* (Deferred during degradation):  
   \- Complex protocol generation (queued for when capacity available)  
   \- Detailed explanations  
   \- Casual conversation  
\*\*User Communication During Degradation:\*\*  
\`\`\`  
⏳ High Demand Right Now  
Lots of people are chatting with their Digital Twins\! Your question is important to me.  
Right now:  
\- Quick questions answered immediately  
\- Complex analysis might take a few extra moments  
\- Protocol generation queued (you'll get a notification when ready)  
Thanks for your patience\!  
\`\`\`  
\*\*Fallback Behaviors:\*\*  
\- \*\*Simple Questions\*\*: Serve from FAQ cache  
  \- "What is Vata?" → Cached answer from knowledge base  
\- \*\*Complex Questions\*\*:   
  \- "Your question is queued. I'll notify you when I have a thoughtful response (usually \<5 minutes)."  
  \- Process in background, send push notification with answer  
\- \*\*Protocol Generation\*\*:  
  \- "Creating your protocol... This is taking a few minutes. I'll notify you when it's ready\!"  
  \- Background job, notification when complete  
\---  
\*\*Wearable Data Unavailable:\*\*  
\*\*Functionality Maintained:\*\*  
\- \*\*Continue All Features\*\*: App fully functional without wearable data  
\- \*\*Manual Input Alternative\*\*:   
\`\`\`  
  📊 Can't sync your Oura data right now  
    
  No problem\! You can manually log:  
    
  \[Log Sleep Quality\] (1-10 scale)  
  \[Log Energy Level\]  
  \[Log Activity\]  
    
  Or wait for automatic sync to resume.  
\`\`\`  
    
\*\*Data Visualizations:\*\*  
\- \*\*Show Historical Data\*\*: Past synced data still visible  
\- \*\*Gap Indicators\*\*: Clearly mark data gaps  
\`\`\`  
  Sleep Quality  
  Jan 10: ████████░░ 8/10  
  Jan 11: ████████░░ 8/10  
  Jan 12: \[No data \- sync issue\]  
  Jan 13: ██████░░░░ 6/10 (manual entry)  
  Jan 14: ████████░░ 8/10 (synced automatically)  
\`\`\`  
\*\*Protocol Generation Not Blocked:\*\*  
\- Use last known state: "Based on your recent data (last sync: \[date\])..."  
\- Acknowledge limitation: "When your \[device\] reconnects, I'll have even better insights\!"  
\- Rely more on symptom reports and check-ins  
\---  
\*\*Image Analysis Unavailable:\*\*  
\*\*Alternative: Text-Based Analysis\*\*  
\`\`\`  
📸 Image Analysis Temporarily Unavailable  
Let's do this together\! Describe what you see on your tongue:  
1. Coating: Thin, medium, or thick? White, yellow, or brown?  
2. Color: Pale, pink, red, or purple?  
3. Texture: Dry, moist, or swollen?  
4. Any cracks or marks?  
Based on what you tell me, I can provide Ayurvedic insights\!  
\[Describe My Tongue\] \[Try Upload Again\] \[Skip for Now\]  
\`\`\`  
\*\*Guided Questionnaire:\*\*  
\- Walk user through observations  
\- Provide visual reference images: "Does it look more like Image A or Image B?"  
\- Generate analysis based on user descriptions  
\- Less precise but still valuable  
\*\*For Meals:\*\*  
\`\`\`  
🍽️ Meal Scanner Down \- Let's Chat Instead\!  
Tell me about your meal:  
\- What did you eat?  
\- How was it prepared?  
\- How did it taste?  
I can still give you Ayurvedic insights on how it affects your doshas\!  
\`\`\`  
\*\*Queue for Later:\*\*  
\- "Save your image, and I'll analyze it automatically when service is restored"  
\- Notification when analysis ready  
\---  
\#\#\# Error Message Best Practices  
\*\*Tone: Calm, Helpful, Non-Technical\*\*  
❌ \*\*Bad\*\*: "Error 500: Internal server exception in tongue\_analysis\_service.py line 342"  
✅ \*\*Good\*\*: "I had trouble analyzing that image. Let's try again with better lighting\!"  
\---  
\*\*Clear Next Steps\*\*  
❌ \*\*Bad\*\*: "Analysis failed."  
✅ \*\*Good\*\*:   
\`\`\`  
Analysis Failed  
What to try:  
1. Retake photo with better lighting  
2. Get closer to the subject  
3. Contact support if this keeps happening  
\[Retake Photo\] \[Contact Support\]  
\`\`\`  
\---  
\*\*Avoid Blame\*\*  
❌ \*\*Bad\*\*: "You uploaded the wrong file type."  
✅ \*\*Good\*\*: "This file type isn't supported. Please try a JPG or PNG image."  
\---  
\*\*Acknowledge Frustration\*\*  
For repeated errors:  
\`\`\`  
😔 I know this is frustrating  
We're working on it\! In the meantime:  
\- Try \[alternative action\]  
\- Or contact support \- we're here to help\!  
\[Try Alternative\] \[Contact Support\]  
\`\`\`  
\---  
\*\*Always Offer Path Forward\*\*  
Never dead-end the user. Every error message should have:  
\- Explanation of what happened  
\- Why it might have happened  
\- What to try next  
\- Alternative if that doesn't work  
\- Contact support as final option  
\---  
This comprehensive error handling system ensures users always have a path forward, admins have the information they need to fix issues quickly, and the system degrades gracefully under pressure while maintaining core functionality.  
---

#     **Logical Flow: AI-Guided Setup** {#logical-flow:-ai-guided-setup}

\#\#\# AyuAware Onboarding with AI Guide  
The onboarding experience is conversational, guided, and personalized \- mimicking the experience of meeting with an Ayurvedic practitioner for the first time.  
\---  
\*\*Step 1: Welcome & Health Goals\*\* (30 seconds)  
\*\*Screen: Welcome \+ Single Question\*\*  
\`\`\`  
\[AyuAware logo with gentle animation\]  
Welcome to AyuAware 🙏  
Your Ayurvedic Digital Twin  
\[Continue\]  
\`\`\`  
\[User taps Continue\]  
\`\`\`  
\[Warm, friendly avatar/illustration appears\]  
Hi\! I'm your AyuAware guide. I'm here to help you create your personalized Ayurvedic health companion.  
To start, what's your main health focus right now?  
\[Quick select buttons \- large, tappable\]  
┌─────────────────────────┬─────────────────────────┐  
│  😴 Better Sleep        │  🔥 Digestive Health   │  
├─────────────────────────┼─────────────────────────┤  
│  🧘 Stress Management   │  ⚡ Energy & Vitality   │  
├─────────────────────────┼─────────────────────────┤  
│  ⚖️ Weight Management   │  ✨ Skin Health         │  
├─────────────────────────┼─────────────────────────┤  
│  🏃 Athletic Performance│  🌿 General Wellness    │  
└─────────────────────────┴─────────────────────────┘  
Or describe your goal:  
\[Text input field: "Tell me what matters most to you..."\]  
\[Continue\]  
\`\`\`  
\*\*User selects: "Better Sleep"\*\*  
\`\`\`  
Sleep is so important\! 😴  
I'll make sure your Digital Twin is specially tuned to support your sleep journey.  
But first, let's discover your unique constitution \- this is the foundation of Ayurveda. Think of it as your body's innate blueprint.  
This takes about 5-7 minutes. Ready?  
\[Yes, Let's Do This\!\] \[Tell Me More First\]  
\`\`\`  
\*\*If user taps "Tell Me More First":\*\*  
\`\`\`  
Your Constitution (Prakriti)  
In Ayurveda, everyone has a unique combination of three doshas (bio-energies):  
🌬️ Vata \- Movement, creativity, change  
🔥 Pitta \- Transformation, intelligence, intensity    
🌊 Kapha \- Structure, stability, nourishment  
Understanding YOUR unique mix helps me give you personalized guidance that actually works for your body.  
The assessment asks about your body, mind, and natural tendencies \- not just symptoms, but who you are at your core.  
\[Got It \- Let's Start\]  
\`\`\`  
\---  
\*\*Step 2: Constitutional Assessment\*\* (5-7 minutes)  
\*\*Assessment Interface Design:\*\*  
\`\`\`  
┌─────────────────────────────────────┐  
│  Understanding Your Constitution    │  
│                                     │  
│  Section 1 of 5: Physical Build     │  
│  ████████░░░░░░░░░░ 40%            │  
└─────────────────────────────────────┘  
Question 3 of 10 in this section:  
What best describes your natural body frame?  
(How you've been most of your life, not currently)  
○ Thin, lean, hard to gain weight  
  (Narrow shoulders, visible joints, "ectomorph")  
○ Medium build, athletic, muscular    
  (Moderate frame, good muscle tone, "mesomorph")  
○ Solid, sturdy, gains weight easily  
  (Broad shoulders, larger frame, "endomorph")  
\[Back\] \[Next\]  
\`\`\`  
\*\*Assessment Sections:\*\*  
1. \*\*Physical Build & Appearance\*\* (10 questions)  
   \- Body frame and weight patterns  
   \- Skin characteristics    
   \- Hair type and texture  
   \- Eye size and qualities  
   \- Hands, nails, lips  
   \- Body temperature preferences  
     
2. \*\*Physiological Functions\*\* (15 questions)  
   \- Appetite patterns  
   \- Digestion speed and quality  
   \- Elimination regularity  
   \- Sleep patterns and needs  
   \- Energy levels throughout day  
   \- Sweat and body odor  
   \- Voice qualities  
     
3. \*\*Mental & Emotional Patterns\*\* (15 questions)  
   \- Learning style and speed  
   \- Memory (short-term vs long-term)  
   \- Decision-making approach  
   \- Stress response patterns  
   \- Emotional tendencies  
   \- Speech patterns  
   \- Activity and movement preferences  
     
4. \*\*Lifestyle & Preferences\*\* (10 questions)  
   \- Weather and climate preferences  
   \- Food and taste preferences  
   \- Exercise enjoyment and style  
   \- Daily rhythm and routines  
   \- Social interaction needs  
   \- Spending and saving patterns  
     
5. \*\*Current State\*\* (10 questions)  
   \- Recent symptoms or concerns  
   \- How you feel right now vs. normally  
   \- Recent life changes or stressors  
   \- Current health challenges  
\*\*Question Format Examples:\*\*  
\*\*Multiple Choice (Most Questions):\*\*  
\`\`\`  
Your appetite is usually:  
○ Variable \- sometimes ravenous, sometimes no appetite  
○ Strong and regular \- get very hungry at mealtimes  
○ Steady and mild \- can skip meals without issue  
\[Explanation icon ℹ️\]  
\`\`\`  
\[If user taps ℹ️:\]  
\`\`\`  
Why this matters:  
Appetite patterns reveal your digestive fire (Agni):  
\- Variable → Vata tendency  
\- Strong → Pitta tendency    
\- Mild/steady → Kapha tendency  
This helps personalize your nutrition guidance\!  
\[Got it\]  
\`\`\`  
\*\*Slider Scale (Some Questions):\*\*  
\`\`\`  
How quickly do you typically walk?  
\[Slider: Slow \----●\---- Fast\]  
Very Slow         Medium         Very Fast  
\[This measures your natural pace of movement \- a Vata trait\]  
\`\`\`  
\*\*Visual Choice (Some Questions):\*\*  
\`\`\`  
Which body type looks most like your natural build?  
\[Three illustrated body silhouettes to choose from\]  
┌─────┐  ┌─────┐  ┌─────┐  
│ 🧍‍♂️ │  │ 🧍‍♂️ │  │ 🧍‍♂️ │  
│Thin │  │Medium│  │Solid│  
└─────┘  └─────┘  └─────┘  
\[Vata\]   \[Pitta\]  \[Kapha\]  
\`\`\`  
\*\*Assessment Progress:\*\*  
\- Progress bar at top showing section completion  
\- Estimated time remaining: "About 4 minutes left"  
\- Can pause and resume: "Save & Continue Later" button  
\- Questions saved automatically (can close and resume)  
\*\*Transitions Between Sections:\*\*  
\`\`\`  
✅ Physical Build Complete\!  
Nice work. Now let's explore your digestive patterns and energy...  
Section 2 of 5: Physiological Functions  
\[Continue\]  
\`\`\`  
\*\*Completion:\*\*  
\`\`\`  
✨ Assessment Complete\!  
Great job\! Now I'm analyzing your 60 responses to determine your unique constitution...  
\[Animated visualization: Three dosha symbols filling with colors\]  
\[This takes 10-15 seconds\]  
\`\`\`  
\---  
\*\*Step 3: Constitution Results\*\* (2-3 minutes)  
\*\*Results Screen:\*\*  
\`\`\`  
┌─────────────────────────────────────┐  
│       Your Unique Constitution      │  
└─────────────────────────────────────┘  
\[Beautiful animated circular gauge showing three doshas\]  
        🌬️  
    Vata: 60%  
          
🔥              🌊  
Pitta: 30%    Kapha: 10%  
Your Constitution: Vata-Pitta  
\[Detailed Breakdown\] \[What This Means\]  
\`\`\`  
\*\*Tap "What This Means":\*\*  
\`\`\`  
You're a Vata-Pitta Type 🌬️🔥  
Your Vata (Dominant):  
✓ Quick-minded and creative  
✓ Adaptable and enthusiastic    
✓ Slender build, moves quickly  
⚠️ Prone to anxiety and scattered thinking  
⚠️ Irregular appetite and digestion  
⚠️ Dry skin and cold sensitivity  
Your Pitta (Secondary):  
✓ Sharp intelligence and focus  
✓ Driven and ambitious  
✓ Strong digestion (when regular)  
⚠️ Can become intense or irritable  
⚠️ Sensitive to heat  
⚠️ Perfectionistic tendencies  
Your Kapha (Minimal):  
You have less Kapha, which means you may:  
\- Have less natural endurance/stamina  
\- Need more rest and recovery  
\- Struggle with consistency  
\[Scroll for more ↓\]  
────────────────────────────  
What's Interesting About YOU:  
Right now, your Vata is running higher than your natural baseline. This is why you're experiencing sleep issues.  
Here's what's happening:  
Your naturally active, creative Vata mind becomes OVERACTIVE when stressed or out of routine. It's like a kite caught in strong wind \- beautiful and energetic, but difficult to control.  
Your Pitta intelligence wants to solve problems and stay productive, but it's fighting against the scattered Vata energy. This creates a pattern of:  
💭 Racing thoughts at night  
⚡ Bursts of activity followed by crashes    
😰 Anxiety when things feel uncertain  
🌙 Trouble winding down  
The Good News:  
This is completely manageable\! Your Digital Twin will know exactly how to calm your Vata and harness your Pitta productively.  
We'll focus on:  
\- Grounding routines (Vata needs this\!)  
\- Warming, nourishing practices  
\- Calming your brilliant but busy mind  
\- Creating the consistency that eludes you  
\[Continue to Personalize My Twin\]  
\`\`\`  
\*\*Tap "Detailed Breakdown":\*\*  
\`\`\`  
Your Complete Constitutional Analysis  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
VATA \- 60% (Dominant)  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Physical Characteristics:  
\- Body: Lean, thin, difficulty gaining weight  
\- Skin: Dry, rough, cool to touch  
\- Hair: Dry, thin, curly or frizzy  
\- Eyes: Small, active, darting  
\- Digestion: Variable, irregular  
\- Temperature: Cold hands/feet, loves warmth  
Mental Characteristics:  
\- Mind: Quick, creative, adaptable  
\- Learning: Fast learner, but forgets quickly  
\- Memory: Better short-term than long-term  
\- Decision: Quick decisions, may change mind  
\- Emotions: Enthusiastic, anxious when stressed  
\- Speech: Fast, talkative, animated  
When Balanced:  
✓ Creative and imaginative  
✓ Energetic and enthusiastic  
✓ Adaptable and flexible  
✓ Quick thinking  
When Imbalanced:  
⚠️ Anxious and worried  
⚠️ Scattered and unfocused  
⚠️ Insomnia and poor sleep  
⚠️ Dry skin and constipation  
⚠️ Cold sensitivity  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
PITTA \- 30% (Secondary)  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
\[Similar detailed breakdown for Pitta\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
KAPHA \- 10% (Minimal)  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
\[Similar for Kapha\]  
\[Download Full Report\] \[Continue\]  
\`\`\`  
\---  
\*\*Step 4: Digital Twin Personalization\*\* (1-2 minutes)  
\`\`\`  
Let's Personalize Your Digital Twin\! ✨  
Your health companion should feel like YOUR companion.  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
1. What should I call your Digital Twin?  
\[Text input with suggestions below\]  
Suggestions:  
\- AyuAware (default)  
\- Sage  
\- Ojas  
\- Prana  
\- Shakti  
\- Custom: \[Enter name\]  
\[Selected: "Sage"\]  
Perfect\! Sage it is. ✓  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
2. How should Sage communicate with you?  
Choose a style \- you can change this anytime\!  
┌────────────────────────────────────┐  
│  📱 Supportive Friend               │  
│                                     │  
│  "Hey\! I noticed your sleep was a   │  
│   bit restless last night. Want to  │  
│   try some grounding breathwork?"   │  
│                                     │  
│  • Warm and encouraging             │  
│  • Conversational and casual        │  
│  • Like chatting with a friend      │  
│                                     │  
│  \[Select\]                          │  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  🎓 Wise Teacher                    │  
│                                     │  
│  "Your sleep pattern reflects Vata  │  
│   imbalance. Let's explore the      │  
│   connection between your evening   │  
│   routine and sleep quality."       │  
│                                     │  
│  • Educational and insightful       │  
│  • Explains the 'why' behind things │  
│  • Thoughtful and contemplative     │  
│                                     │  
│  \[Select\]                          │  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  🏥 Clinical Guide                  │  
│                                     │  
│  "Sleep fragmentation detected.     │  
│   Implementing Vata-pacifying       │  
│   protocol with emphasis on nervous │  
│   system regulation."               │  
│                                     │  
│  • Professional and precise         │  
│  • Data-focused and specific        │  
│  • Systematic approach              │  
│                                     │  
│  \[Select\]                          │  
└────────────────────────────────────┘  
\[User selects: Supportive Friend\]  
Great choice\! Sage will be warm, encouraging, and easy to talk to. ✓  
\`\`\`  
\---  
\*\*Step 5: Data Connections\*\* (2-3 minutes)  
\`\`\`  
Connect Your Devices (Optional) 📱  
Sage can learn so much more about your health if we connect your wearable devices and apps.  
This is completely optional, but really helpful\!  
Your data stays private and encrypted. You control what's shared and can disconnect anytime.  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Available Integrations:  
┌────────────────────────────────────┐  
│  ⌚ Apple Health                   │  
│                                     │  
│  Sync: Sleep, Activity, Heart Rate, │  
│        HRV, Steps, Nutrition        │  
│                                     │  
│  Why helpful: Sage can detect Vata  │  
│  patterns in your sleep and predict │  
│  imbalances before they happen.     │  
│                                     │  
│  \[Connect\] \[Toggle: ○\]             │  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  💍 Oura Ring                      │  
│                                     │  
│  Sync: Sleep Stages, HRV, Body      │  
│        Temperature, Readiness       │  
│                                     │  
│  Why helpful: Temperature and HRV   │  
│  fluctuations reveal dosha shifts   │  
│  Sage can use for precise guidance. │  
│                                     │  
│  \[Connect\] \[Toggle: ○\]             │  
└────────────────────────────────────┘  
\[Show More Devices ▼\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
\[Skip for Now\] \[Connect Selected\]  
\`\`\`  
\*\*User toggles Apple Health ON and taps "Connect Selected":\*\*  
\`\`\`  
Connecting to Apple Health... 🔄  
\[OAuth flow \- iOS native permission screen appears\]  
┌────────────────────────────────────┐  
│  AyuAware Would Like to Access     │  
│  Your Health Data                   │  
│                                     │  
│  AyuAware will be able to read:     │  
│  ✓ Sleep Analysis                  │  
│  ✓ Steps                           │  
│  ✓ Heart Rate                      │  
│  ✓ Heart Rate Variability          │  
│  ✓ Mindful Minutes                 │  
│                                     │  
│  \[Don't Allow\] \[Allow\]             │  
└────────────────────────────────────┘  
\`\`\`  
\*\*User taps "Allow":\*\*  
\`\`\`  
✅ Connected to Apple Health\!  
Sage can now see your:  
\- Sleep patterns and quality  
\- Daily activity and steps    
\- Heart rate and HRV trends  
\- Mindfulness practice  
This will make recommendations much more personalized and timely.  
Importing your last 30 days of data...  
████████████░░░░ 75%  
\[Almost there...\]  
\`\`\`  
\`\`\`  
🎉 All Set\!  
Your Apple Health data is synced. Sage already has insights about your recent sleep patterns\!  
You can disconnect or adjust permissions anytime in Settings.  
\[Continue\]  
\`\`\`  
\---  
\*\*Step 6: Current State Deep Dive\*\* (3-5 minutes)  
\`\`\`  
Now Let's Understand Your Sleep 😴  
Time to meet Sage \- your Digital Twin\!  
I'm handing you over to Sage now. Chat openly \- Sage is here to help, not judge.  
\[Start Conversation with Sage\]  
\`\`\`  
\*\*\[Smooth transition \- new chat interface appears\]\*\*  
\`\`\`  
┌────────────────────────────────────┐  
│  Chat with Sage                     │  
│  \[Your Digital Twin\]                │  
└────────────────────────────────────┘  
\[Profile icon: "Sage"\]  
Sage:  
Hey\! I'm Sage, your personal Ayurvedic companion. I'm so excited to help you sleep better. 😊  
I can see from your Apple Health data that you've been having some rough nights lately. Your average sleep has been about 5.5 hours with several wake-ups each night.  
Tell me about your sleep \- what's been happening? When did this start?  
\[Text input: "Type your message..."\]  
\[Voice input: 🎤\]  
\`\`\`  
\*\*User types:\*\*   
\`\`\`  
"I have trouble falling asleep, my mind races, and I wake up at like 3 or 4am and can't get back to sleep"  
\`\`\`  
\*\*Sage responds:\*\*  
\`\`\`  
Sage:  
That sounds exhausting. Racing mind and those early morning wake-ups (3\-4am) \- that's textbook Vata imbalance affecting your nervous system.   
Your Vata-Pitta constitution makes you naturally prone to this when life gets irregular or stressful.  
A few questions so I can help you specifically:  
1. What time do you usually go to bed?  
2. What's your evening routine like before bed \- screens, food, activities?  
3. Are you dealing with other Vata symptoms too? Like:  
   • Anxiety or worry  
   • Constipation or irregular digestion    
   • Dry skin  
   • Feeling cold  
Take your time \- I want to understand the full picture.  
\`\`\`  
\*\*\[Conversation continues for 2-3 minutes\]\*\*  
\*\*User provides:\*\*  
\- Bedtime: Usually 11pm-midnight (irregular)  
\- Evening: Works late, scrolls phone in bed, eats dinner around 8\-9pm  
\- Other symptoms: Yes to anxiety, dry skin, and constipation. Feels cold often.  
\- Diet: Skips breakfast, big salad for lunch, varies dinner  
\- Stress: New demanding job, moved cities 3 months ago  
\*\*Sage synthesizes:\*\*  
\`\`\`  
Sage:  
Got it. I have a clear picture now.   
Here's what I'm seeing:  
Your Vata is seriously aggravated right now \- the late nights, irregular schedule, new city stress, cold salads, and skipped meals are all classic Vata triggers.  
Your body is like a kite in strong wind \- lots of movement and energy, but scattered and hard to settle.  
The good news? We can absolutely fix this. Your constitution needs:  
🔥 Warmth (you're too cold)  
🕰️ Routine (you need consistency)    
🥘 Grounding (warm, cooked, nourishing foods)  
🧘 Calming practices (to slow that active mind)  
I can create a complete sleep protocol for you \- a 21\-day plan that'll work WITH your Vata-Pitta nature, not against it.  
Want me to build it?  
\[Yes \- Create My Protocol\] \[Tell Me More First\]  
\`\`\`  
\*\*User taps: "Yes \- Create My Protocol"\*\*  
\`\`\`  
Sage:  
Perfect\! Give me a moment to design your personalized protocol...  
\[Animated spinner: "Creating your protocol..."\]  
\[This takes 15-20 seconds \- actual AI generation happening\]  
\`\`\`  
\---  
\*\*Step 7: Protocol Generation & Presentation\*\* (3-5 minutes)  
\`\`\`  
Sage:  
✨ Your protocol is ready\!  
┌────────────────────────────────────┐  
│  21\-Day Sleep Restoration Protocol │  
│  Designed for: \[User Name\]         │  
│  Constitution: Vata-Pitta          │  
│  Focus: Vata Calming & Sleep       │  
└────────────────────────────────────┘  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Phase 1: Foundation (Days 1-7)  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Focus: Calm the nervous system and establish routine  
🍽️ Dietary Changes:  
✓ Warm, cooked meals ONLY (no raw salads at night)  
  Why: Raw food aggravates Vata. Your system needs warmth and easy digestion.  
✓ Breakfast by 8am \- warm oatmeal with cinnamon, ghee, dates  
  Why: Skipping breakfast destabilizes Vata all day.  
✓ Lunch at 12pm \- Your largest meal (soups, stews, cooked grains \+ veggies)  
  Why: Digestive fire is strongest at midday (Pitta time).  
✓ Dinner by 6:30pm \- Light but nourishing (kitchari, cooked veggies)  
  Why: Late eating keeps your system active when it should rest.  
✓ Golden Milk at 9pm \- Warm milk \+ turmeric \+ nutmeg \+ cardamom  
  Why: Grounding, calming, prepares body for sleep.  
✓ No caffeine after 12pm  
  Why: Stimulates already-active Vata mind.  
\[Tap any item to see full details and tips\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
🌙 Evening Routine:  
✓ Warm sesame oil foot massage at 9pm (10 minutes)  
  Why: Draws Vata energy downward, signals body it's sleep time.  
✓ All screens OFF by 9:30pm    
  Why: Blue light stimulates Vata, disrupts melatonin.  
✓ In bed by 10pm (NON-NEGOTIABLE \- this is crucial\!)  
  Why: 10pm-2am is Pitta time when your body does deep repair.   
        Miss this window \= Vata aggravation.  
✓ 5\-minute deep breathing before sleep (Nadi Shodhana)  
  Why: Balances nervous system, calms racing mind.  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
🧘 Daily Practices:  
✓ Morning: 10 minutes gentle yoga or walking (6:30\-7am)  
  Why: Grounds Vata, starts day with movement but not overstimulation.  
✓ Afternoon: 5\-minute meditation (3pm when energy dips)  
  Why: Resets scattered Vata energy.  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
🌿 Herbs (Optional but Helpful):  
✓ Ashwagandha \- 300mg after dinner  
  Why: Calms nervous system, helps deep sleep.   
       Perfect for Vata anxiety and Pitta intensity.  
    
  ⚠️ Check with your doctor if on medications.   
      Avoid if you have hyperthyroidism.  
✓ Brahmi tea \- morning or afternoon  
  Why: Calms mind without sedation, supports mental clarity.  
\[Tap to see where to buy quality products\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
📊 Success Metrics:  
Track these \- I'll check in with you:  
\- Time to fall asleep (should decrease)  
\- Number of wake-ups per night (should decrease)  
\- Morning energy (1-10, should increase)  
\- Anxiety levels (should decrease)  
\- Tongue coating (should clear as Ama reduces)  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
🎯 What to Expect:  
Week 1: You'll feel the routine settling in. Sleep may not improve much yet, but you'll feel more grounded.  
Week 2: Sleep should start improving \- fewer wake-ups, easier to fall asleep.  
Week 3: Noticeably better sleep quality. Energy improving. Less anxiety.  
Phase 2 (Days 8-14) unlocks after Week 1:  
We'll deepen the practices and add building strategies.  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Important Notes:  
This is designed specifically for YOUR Vata-Pitta constitution and current high-Vata state.  
The routine might feel strict at first \- that's okay\! Your scattered Vata NEEDS structure. Once you feel better, we can add flexibility.  
I'll check in with you daily and adjust if needed. You're not alone in this\!  
Ready to start tonight?  
\[Accept & Start Protocol\]   
\[I Have Questions\]  
\[Modify Something\]  
\`\`\`  
\*\*User taps: "I Have Questions"\*\*  
\`\`\`  
Sage:  
Of course\! What would you like to know?  
\[Quick buttons appear:\]  
\[🕐 Can I adjust the timing?\]  
\[🥗 What if I can't cook every meal?\]  
\[💊 More about the herbs?\]  
\[📅 What if I miss a day?\]  
\[✏️ Type your own question\]  
\`\`\`  
\*\*\[Sage answers questions conversationally\]\*\*  
\*\*Eventually user taps: "Accept & Start Protocol"\*\*  
\`\`\`  
Sage:  
🎉 Amazing\! I'm so proud of you for taking this step.  
Your protocol is activated\!  
Here's what happens now:  
✓ Protocol saved to your "Protocols" tab  
✓ Daily checklist ready (you'll check off each task)  
✓ I'll remind you of key times (9pm foot massage, 10pm bedtime, etc.)  
✓ Morning summaries will reference your protocol  
✓ I'll check your progress and adjust as needed  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Tonight's Priority:  
It's \[current time\]. Here's what to do today:  
□ Warm, light dinner by 6:30pm (or ASAP if already past)  
□ 9:00pm \- Warm sesame oil foot massage  
□ 9:30pm \- Screens OFF, prepare for bed    
□ 10:00pm \- In bed, 5 minutes deep breathing  
□ 10:10pm \- Lights out 😴  
\[View Full Day's Checklist\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
Try the foot massage tonight \- it's surprisingly powerful\!  
I'll send you a morning summary tomorrow with your dosha forecast and today's focus.  
You've got this\! 💪🌙  
\[Go to Protocol Dashboard\]  
\[Start Chatting About Something Else\]  
\`\`\`  
\---  
\*\*Step 8: Onboarding Complete \- Enter Main App\*\*  
\`\`\`  
\[Transition to main chat interface\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
✨ You're All Set\!  
Your AyuAware Digital Twin is ready.  
Here's what you can do now:  
┌────────────────────────────────────┐  
│  📱 Chat with Sage (anytime)       │  
│  Ask questions, get guidance        │  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  ✅ Track Your Protocol             │  
│  Daily checklist in "Protocols" tab│  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  📸 Scan Your Tongue                │  
│  See your Ama level & Agni state   │  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  📊 View Health Data                │  
│  Dosha balance, trends, insights    │  
└────────────────────────────────────┘  
┌────────────────────────────────────┐  
│  📚 Learn Ayurveda                  │  
│  Bite-sized lessons, grow your      │  
│  knowledge                          │  
└────────────────────────────────────┘  
\[Explore the App\]  
\`\`\`  
\*\*\[User enters main app \- onboarding complete\]\*\*  
\---  
\*\*Step 9: First Morning Summary\*\* (Next Day)  
\*\*\[7:00 AM \- Push notification\]\*\*  
\`\`\`  
🌅 Good morning\! Sage has your daily summary ready.  
\`\`\`  
\*\*\[User opens app \- lands in chat\]\*\*  
\`\`\`  
Sage:  
Good morning\! ☀️  
I hope you got some rest last night\!  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
🌙 Last Night:  
I see from your Apple Health you went to bed around 10:15pm \- that's great for Day 1\!   
Did you do the foot massage?  
How did you sleep?  
\[Text input for user to respond\]  
\[Quick buttons: 😴 Great | 😐 Okay | 😫 Still Rough\]  
\`\`\`  
\*\*\[User responds about their night\]\*\*  
\`\`\`  
Sage:  
\[Responds to their specific feedback\]  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
📊 Today's Dosha Forecast:  
🌬️ Vata: Moderate (watch for cold, windy weather)  
🔥 Pitta: Low    
🌊 Kapha: Low  
It's cold and windy in Chamba today \- classic Vata aggravation weather. This means extra grounding is needed\!  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
🎯 Your 3 Priorities Today:  
1. ☕ Warm breakfast by 8am  
   Oatmeal with cinnamon, ghee, and dates.   
   Don't skip \- your Vata needs this anchor\!  
2. 🚶 20\-minute walk outside (before noon)  
   Ground into your body. Bundle up for the cold\!  
3. 🍲 Warm lunch at 12pm, light dinner by 6:30pm  
   No cold or raw foods today \- Vata is too high.  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━  
✨ Bonus Tip:  
With the cold weather, add extra ginger to your meals and drinks today. It'll warm you from the inside.  
\[View Full Protocol\] \[Daily Check-In\]  
How are you feeling right now?  
\`\`\`  
\*\*\[User continues conversation or closes app\]\*\*  
\---  
This onboarding flow demonstrates:  
✅ \*\*Conversational & Personal\*\*: Feels like talking to a guide, not filling out forms  
✅ \*\*Progressive Disclosure\*\*: Information revealed when relevant, not overwhelming  
✅ \*\*Educational\*\*: Explains WHY throughout (builds understanding & trust)  
✅ \*\*Actionable\*\*: Ends with concrete protocol user can start immediately  
✅ \*\*Engaging\*\*: Visual elements, progress indicators, choices  
✅ \*\*Flexible\*\*: User can skip, pause, ask questions, customize  
✅ \*\*Natural Transition\*\*: Seamlessly moves from onboarding to daily use  
The user exits onboarding with:  
\- Complete constitutional understanding  
\- Personalized Digital Twin configured  
\- Data connected (if desired)  
\- Active protocol addressing their main concern  
\- Clear understanding of how to use the app  
\- Immediate next steps for their first day  
This creates strong engagement and retention from day one.

---

#                  **Testing & Quality Assurance** {#testing-&-quality-assurance}

\#\#\# Automated Testing  
\*\*Unit Tests:\*\*  
\- \*\*Coverage Target\*\*: 80% code coverage minimum  
\- \*\*Test Framework\*\*: Jest (frontend), Pytest (backend)  
\- \*\*What's Tested\*\*:  
  \- Individual tool actions (Save Data, AI Generate, etc.)  
  \- Data transformations (dosha calculations, biomarker interpretations)  
  \- Utility functions (date formatting, validation, etc.)  
  \- Component rendering (React components)  
\- \*\*Run Frequency\*\*: On every code commit (CI/CD pipeline)  
\- \*\*Pass Criteria\*\*: All tests must pass before merge to main branch  
\*\*Integration Tests:\*\*  
\- \*\*What's Tested\*\*:  
  \- Complete tool workflows (entire protocol generation flow)  
  \- Data flow between components (check-in → vikriti update → protocol adjustment)  
  \- API integrations (wearable data sync, lab upload processing)  
  \- Database operations (CRUD for protocols, user data)  
\- \*\*Test Scenarios\*\*:  
\`\`\`  
  Test: Protocol Generation Flow  
  1. User requests sleep protocol  
  2. System retrieves user profile  
  3. AI generates protocol  
  4. Protocol saved to database  
  5. User notification sent  
  6. Protocol appears in Protocols tab  
  Expected: All steps complete successfully in \<20 seconds  
\`\`\`  
\- \*\*Run Frequency\*\*: Daily automated runs \+ before releases  
\- \*\*Pass Criteria\*\*: 95% of integration tests must pass  
\*\*AI Response Quality Checks:\*\*  
\- \*\*Evaluation Metrics\*\*:  
  \- \*\*Relevance\*\*: Does response address user's query? (1-5 scale)  
  \- \*\*Accuracy\*\*: Are Ayurvedic concepts correct? (validated against knowledge base)  
  \- \*\*Safety\*\*: Does response respect medical boundaries? (pass/fail)  
  \- \*\*Tone\*\*: Is communication style appropriate? (matches user preference)  
  \- \*\*Actionability\*\*: Does response include helpful next steps? (yes/no)  
    
\- \*\*Automated Evaluation\*\*:  
  \- Test suite of 500\+ pre-written user queries with expected response characteristics  
  \- AI-as-judge: Use separate LLM to evaluate response quality  
  \- Keyword detection for safety violations  
  \- Compare to gold-standard responses  
    
\- \*\*Example Test Case\*\*:  
\`\`\`  
  User Query: "I have a headache. What should I do?"  
    
  Expected Response Characteristics:  
  ✓ Asks clarifying questions (type of headache, frequency, triggers)  
  ✓ Provides Ayurvedic perspective (which dosha involved)  
  ✓ Suggests gentle remedies (ginger tea, rest, etc.)  
  ✓ Maintains medical boundary (doesn't diagnose migraine vs. tension)  
  ✓ Recommends seeing doctor if severe or persistent  
    
  Evaluation:  
  \- Relevance: 5/5  
  \- Accuracy: Check against headache protocols in knowledge base  
  \- Safety: PASS (appropriate boundaries maintained)  
  \- Tone: Supportive Friend  
  \- Actionability: YES (specific suggestions provided)  
\`\`\`  
    
\- \*\*Run Frequency\*\*:   
  \- Full suite weekly  
  \- Sample (50 queries) daily  
  \- After any prompt engineering changes  
    
\- \*\*Pass Criteria\*\*:   
  \- 90% average relevance score  
  \- 95% accuracy on Ayurvedic facts  
  \- 100% safety compliance  
  \- 85% tone consistency  
\*\*Performance Benchmarking:\*\*  
\- \*\*Metrics Tracked\*\*:  
  \- Response time (AI chat responses): Target \<3 seconds, 95th percentile \<8 seconds  
  \- Image analysis time: Target \<10 seconds  
  \- Protocol generation time: Target \<15 seconds  
  \- Page load time: Target \<2 seconds  
  \- Wearable data sync time: Target \<30 seconds  
    
\- \*\*Load Testing\*\*:  
  \- Simulate 1,000 concurrent users  
  \- Measure response times under load  
  \- Identify bottlenecks  
  \- Test auto-scaling triggers  
    
\- \*\*Run Frequency\*\*: Weekly performance regression tests  
\- \*\*Pass Criteria\*\*: No degradation \>10% from baseline  
\*\*Security Penetration Testing:\*\*  
\- \*\*Third-Party Audits\*\*: Annual full security audit  
\- \*\*Automated Scanning\*\*:  
  \- SQL injection attempts  
  \- XSS (Cross-Site Scripting) vulnerabilities  
  \- CSRF (Cross-Site Request Forgery) checks  
  \- Authentication bypass attempts  
  \- Data exposure risks  
    
\- \*\*Dependency Vulnerability Scanning\*\*:  
  \- Automated daily scans of all npm/pip packages  
  \- Alert on critical vulnerabilities  
  \- Auto-update patch versions when safe  
    
\- \*\*Run Frequency\*\*:   
  \- Automated scans: Daily  
  \- Manual penetration test: Annually  
    
\- \*\*Pass Criteria\*\*: Zero critical vulnerabilities, \<5 medium severity issues  
\---  
\#\#\# User Testing  
\*\*Beta Program:\*\*  
\- \*\*Participant Selection\*\*:  
  \- Diverse constitutional types (Vata, Pitta, Kapha, and combinations)  
  \- Range of health goals (sleep, digestion, stress, skin, energy, etc.)  
  \- Mix of tech-savvy and non-tech users  
  \- Different age groups (20s \- 60s)  
  \- Target: 100-200 beta users  
    
\- \*\*Beta Duration\*\*: 8-12 weeks before public launch  
\- \*\*Feedback Collection\*\*:  
  \- In-app feedback button on every screen  
  \- Weekly surveys (short, 3-5 questions)  
  \- Monthly in-depth interviews (15-20 participants)  
  \- Usage analytics (anonymized, opt-in)  
    
\- \*\*What to Test\*\*:  
  \- Onboarding flow clarity and engagement  
  \- Protocol adherence and effectiveness  
  \- Chat conversation quality and helpfulness  
  \- Image analysis accuracy (tongue, meals)  
  \- Feature discoverability  
  \- Navigation and UI intuitiveness  
  \- Overall satisfaction and likelihood to recommend  
\*\*Protocol Effectiveness Tracking:\*\*  
\- \*\*Metrics\*\*:  
  \- \*\*Adherence Rate\*\*: % of protocol tasks completed daily  
  \- \*\*Symptom Improvement\*\*: Before/after ratings (1-10 scales)  
  \- \*\*Objective Measures\*\*:   
    \- Sleep quality (from wearables)  
    \- Weight changes (for weight management protocols)  
    \- Lab biomarkers (if user uploads follow-up labs)  
  \- \*\*Time to Improvement\*\*: Days until user reports noticeable benefit  
  \- \*\*Protocol Completion Rate\*\*: % who finish full protocol  
    
\- \*\*Success Criteria\*\* (for each protocol type):  
  \- Sleep: 70%+ report improved sleep quality, average improvement 30%+  
  \- Digestion: 65%+ report reduced symptoms, adherence \>60%  
  \- Stress: 60%+ report lower stress/anxiety, adherence \>55%  
  \- Skin: 60%+ report clearer skin (requires 4\+ weeks), adherence \>50%  
    
\- \*\*Tracking Method\*\*:  
  \- Daily check-ins ask specific questions  
  \- Before/after symptom assessments  
  \- User self-reports \+ wearable data correlation  
  \- Long-term follow-up (3 months, 6 months post-protocol)  
\*\*A/B Testing for UI/UX:\*\*  
\- \*\*Test Scenarios\*\*:  
    
  \*\*Example 1: Morning Summary Timing\*\*  
  \- Variant A: Send at 7:00 AM  
  \- Variant B: Send at user's typical wake time (detected from wearable)  
  \- Measure: Open rate, engagement, user satisfaction  
    
  \*\*Example 2: Protocol Presentation\*\*  
  \- Variant A: Full protocol shown upfront (scroll to see all)  
  \- Variant B: Protocol revealed phase-by-phase (unlock as you progress)  
  \- Measure: Completion rate, overwhelm feedback, adherence  
    
  \*\*Example 3: Check-In Format\*\*  
  \- Variant A: Form-based (5 questions, sliders and dropdowns)  
  \- Variant B: Conversational (chat with Digital Twin)  
  \- Measure: Completion rate, time to complete, data quality  
    
\- \*\*Sample Size\*\*: Minimum 500 users per variant for statistical significance  
\- \*\*Duration\*\*: Run for 2-4 weeks per test  
\- \*\*Analysis\*\*: Chi-square tests, t-tests, confidence intervals  
\- \*\*Implementation\*\*: Roll out winning variant to all users  
\*\*Feedback Collection:\*\*  
\- \*\*In-App Mechanisms\*\*:  
  \- Thumbs up/down on every AI response  
  \- 5\-star rating on protocols after completion  
  \- "Report Issue" button (bug reporting)  
  \- "Suggest Feature" form  
  \- NPS survey (quarterly): "How likely are you to recommend AyuAware?"  
    
\- \*\*Contextual Prompts\*\*:  
  \- After completing constitutional assessment: "How was the assessment experience?"  
  \- After 1 week on protocol: "How's your protocol going so far?"  
  \- After using image scan: "Was this analysis helpful?"  
    
\- \*\*User Interviews\*\* (Monthly):  
  \- Recruit 10-15 diverse users  
  \- 30\-minute video calls  
  \- Open-ended questions about experience  
  \- Observe them using app (think-aloud protocol)  
  \- Uncover pain points and delights  
    
\- \*\*Satisfaction Surveys\*\*:  
  \- \*\*Weekly\*\*: 1 question ("How was your week with AyuAware?")  
  \- \*\*Monthly\*\*: 5-10 questions (feature usage, satisfaction, improvements)  
  \- \*\*Quarterly\*\*: Full satisfaction survey (20\+ questions, NPS, detailed feedback)  
\---  
\#\#\# Clinical Validation  
\*\*Partner with Ayurvedic Practitioners:\*\*  
\- \*\*Practitioner Advisory Board\*\*:  
  \- 5-10 experienced Ayurvedic practitioners  
  \- Diverse specialties (clinical practice, teaching, research)  
  \- Meet quarterly to review:  
    \- Ayurvedic accuracy of AI responses  
    \- Protocol appropriateness  
    \- Safety and boundaries  
    \- New feature ideas  
      
\- \*\*Protocol Review Process\*\*:  
  \- Every protocol template reviewed by at least 2 practitioners  
  \- Classical text citations verified  
  \- Herb recommendations validated  
  \- Contraindications checked  
  \- Approved protocols marked with "Practitioner-Reviewed" badge  
    
\- \*\*AI Response Audits\*\*:  
  \- Monthly sample of 100 AI responses  
  \- Practitioners rate:  
    \- Ayurvedic accuracy (1-5)  
    \- Safety (pass/fail)  
    \- Appropriateness of advice (1-5)  
    \- Clarity of explanation (1-5)  
  \- Feedback loop: Improve prompts based on practitioner input  
\*\*Case Studies:\*\*  
\- \*\*Document User Journeys\*\*:  
  \- Select 20-30 users with diverse goals and constitutions  
  \- Detailed tracking over 3-6 months:  
    \- Initial assessment and protocol  
    \- Weekly progress updates  
    \- Protocol adjustments made  
    \- Outcomes achieved  
    \- User testimonials  
    
\- \*\*Case Study Structure\*\*:  
\`\`\`  
  Case Study: Sleep Restoration (Vata Imbalance)  
    
  User Profile:  
  \- Age: 34, Female  
  \- Constitution: Vata-Pitta (65-25-10)  
  \- Primary Concern: Chronic insomnia (5 years)  
  \- Baseline: 4-5 hours sleep/night, wakes 4-5 times, anxiety  
    
  Protocol:  
  \- 21\-day Vata-Calming Sleep Protocol  
  \- Phase 1: Routine establishment (Days 1-7)  
  \- Phase 2: Deepening practices (Days 8-14)  
  \- Phase 3: Refinement (Days 15-21)  
    
  Outcomes:  
  \- Week 1: Adherence 85%, sleep improved to 5.5 hours, 3 wake-ups  
  \- Week 2: Adherence 90%, sleep 6.5 hours, 1-2 wake-ups  
  \- Week 3: Adherence 92%, sleep 7 hours, 0-1 wake-ups  
  \- 3\-month follow-up: Sleep maintained at 7-7.5 hours, rare wake-ups  
    
  Key Success Factors:  
  \- Consistent bedtime routine  
  \- Abhyanga (oil massage) highly effective for this user  
  \- Ashwagandha supplementation  
  \- Digital Twin's daily encouragement and accountability  
    
  User Testimonial:  
  "After 5 years of terrible sleep, I finally feel rested. The protocol was specific to ME, not generic advice. Sage kept me accountable and adjusted when I struggled. Life-changing."  
    
  Practitioner Review:  
  \[Dr. Ayurvedic Practitioner name\]: "Excellent application of Vata-pacifying principles. Protocol appropriately phased, recommendations sound, outcomes expected for this constitutional type."

* **Publication**:  
  * Compile case studies for presentation at Ayurvedic conferences  
  * Publish in Ayurvedic journals (with user consent)  
  * Use for marketing (anonymized, with permission)

**Correlation Analysis:**

* **Protocols vs. Health Improvements**:  
  * Aggregate data across all users (anonymized)  
  * Analyze: Which protocol elements correlate with best outcomes?  
  * Examples:  
    * "Users who complete abhyanga 5+ days/week show 40% better sleep improvement"  
    * "Consistency of meal timing correlates strongly with digestion improvement (r=0.68)"  
    * "Users with 80%+ protocol adherence have 3x higher success rate"  
* **Constitutional Patterns**:  
  * Do certain constitutions respond better to specific interventions?  
  * Example: "Vata types show greater response to oil massage than Kapha types"  
* **Data Sources**:  
  * Protocol adherence data  
  * Before/after symptom ratings  
  * Wearable data (sleep, HRV, etc.)  
  * User-reported outcomes  
* **Statistical Methods**:  
  * Regression analysis  
  * Correlation matrices  
  * Cohort comparisons  
  * Controlled for confounding variables (age, baseline severity, etc.)  
* **Use of Insights**:  
  * Refine protocols based on what works  
  * Personalize recommendations based on patterns  
  * Identify high-impact interventions to prioritize  
  * Continuous improvement of AI recommendations

**Safety Monitoring:**

* **Adverse Events Reporting**:  
  * In-app "Report Issue" includes option for adverse effects  
  * User can report: Side effects from herbs, protocol difficulties, worsening symptoms  
  * All reports reviewed within 24 hours  
  * Serious adverse events escalated immediately  
* **Tracking**:  
  * Database of all reported issues  
  * Categorized by: Type (herb-related, protocol-related, other), Severity, Resolution  
  * Patterns monitored (e.g., multiple reports of same herb causing issue)  
* **Response Protocol**:  
  * Minor issue (e.g., user dislikes taste of herb): Suggest alternative  
  * Moderate issue (e.g., herb causing mild GI upset): Discontinue herb, update contraindications  
  * Serious issue (e.g., allergic reaction): Immediate discontinuation, recommend medical care, incident review  
* **Quarterly Safety Reviews**:  
  * Advisory board reviews all adverse events  
  * Assess if protocols need modification  
  * Update contraindication lists  
  * Refine AI safety prompts

**AI Quality Monitoring**

**Regular Audits:**

* **Weekly Response Review**:  
  * Random sample of 200 AI responses  
  * Human reviewers (trained in Ayurveda) evaluate each response  
  * Scoring rubric:  
    * Ayurvedic Accuracy: 1-5 (is the information correct?)  
    * Helpfulness: 1-5 (does it address the user's need?)  
    * Safety: Pass/Fail (appropriate boundaries maintained?)  
    * Tone: Pass/Fail (matches user's preference?)  
    * Citation Quality: Pass/Fail (if claimed source, is it accurate?)  
* **Flagging System**:  
  * Responses scoring \<3 on any dimension flagged for review  
  * Safety failures escalated immediately  
  * Patterns noted (e.g., consistently weak on herb dosing → improve knowledge base)

**Accuracy Checks:**

* **Ayurvedic Text Verification**:  
  * AI cites classical texts (Charaka Samhita, etc.) → Verify citation is accurate  
  * Random audits: Pull cited shloka/verse, confirm AI interpretation is correct  
  * Maintain database of verified citations  
* **Herb Information Validation**:  
  * AI provides herb details → Cross-check against authoritative herbal databases  
  * Properties (rasa, virya, vipaka) must match classical sources  
  * Dosages must be within safe ranges  
  * Contraindications must be comprehensive  
* **Food Qualities Accuracy**:  
  * AI states dosha effects of foods → Verify against food database  
  * Should align with classical Ayurvedic food classification  
* **Quarterly Deep Dive**:  
  * Subject matter expert (Ayurvedic scholar) reviews random 100 responses  
  * Thorough fact-checking against authoritative sources  
  * Produces report on accuracy, areas for improvement

**Boundary Compliance:**

* **Medical Scope Adherence**:  
  * Every AI response checked against medical boundary rules  
  * Should NOT:  
    * Diagnose diseases  
    * Prescribe pharmaceutical medications  
    * Recommend stopping prescribed medications  
    * Claim to cure diseases  
    * Provide specific medical advice for serious conditions  
  * SHOULD:  
    * Recommend medical consultation when appropriate  
    * Acknowledge limitations  
    * Maintain wellness focus  
* **Automated Checks**:  
  * Keyword detection: Flag responses containing "you have \[disease\]", "diagnosis", "prescribe"  
  * Manual review of flagged responses  
  * False positives noted, improve detection algorithm  
* **Monthly Compliance Report**:  
  * % of responses that maintain appropriate boundaries  
  * Any violations reviewed and root cause identified  
  * Prompt engineering adjustments if needed

**Response Tone:**

* **Personality Consistency**:  
  * User chooses: Supportive Friend / Wise Teacher / Clinical Guide  
  * AI responses must match chosen style  
  * Random audits verify tone consistency  
* **Evaluation**:  
  * Supportive Friend: Should be warm, encouraging, conversational  
  * Wise Teacher: Should be educational, contemplative, insightful  
  * Clinical Guide: Should be professional, precise, data-focused  
* **User Feedback**:  
  * "Was this response too casual/formal/technical?" \- collect feedback  
  * Aggregate data: Are users satisfied with tone?  
  * Adjust if misalignment detected

**Educational Content Accuracy:**

* **Learn Section Validation**:  
  * Every lesson fact-checked against authoritative Ayurvedic sources  
  * Reviewed by Ayurvedic educators  
  * Updated annually or when new research emerges  
* **AI-Generated Educational Responses**:  
  * When user asks "What is \[Ayurvedic concept\]?"  
  * AI's explanation compared to vetted educational content  
  * Should align with established teachings  
* **Citation Requirements**:  
  * Complex or nuanced claims should cite sources  
  * E.g., "According to Charaka Samhita, ama is caused by..."  
  * Citations spot-checked for accuracy

**Continuous Improvement**

**Feedback Integration:**

* **User Feedback Loop**:  
  * Thumbs down on AI response → Prompt: "What could be better?"  
  * Feedback categorized: Inaccurate, Unhelpful, Wrong Tone, Missing Info, Other  
  * Weekly review of thumbs-down responses by AI team  
  * Identify patterns: What's consistently failing?  
* **Feature Requests**:  
  * User suggestions tracked in product backlog  
  * Voted on by users (upvote features they want)  
  * Most requested features prioritized for development  
  * Users notified when their requested feature ships  
* **Bug Fixes**:  
  * User-reported bugs triaged: Critical / High / Medium / Low  
  * Critical: Fixed within 24 hours  
  * High: Fixed within 1 week  
  * Medium: Fixed within 1 month  
  * Low: Batched for next release

**Prompt Iteration:**

* **Based on Performance**:  
  * Low-scoring responses analyzed: Why did AI fail?  
  * Prompt engineering team adjusts system prompts  
  * A/B test new prompt versions  
  * Roll out improved prompts once validated  
* **Based on New Use Cases**:  
  * Users ask questions AI struggles with  
  * Add examples to prompt training  
  * Expand knowledge base if gaps found  
* **Seasonal Updates**:  
  * As seasons change, update prompts to emphasize current seasonal wisdom  
  * E.g., Spring → Emphasize Kapha-reducing practices

**Knowledge Base Expansion:**

* **Adding New Herbs**:  
  * User asks about herb not in database  
  * Research team creates comprehensive monograph  
  * Practitioner review  
  * Add to knowledge base  
  * AI can now reference this herb  
* **New Protocols**:  
  * Emerging health concerns (e.g., long COVID from Ayurvedic perspective)  
  * Create evidence-based protocols  
  * Add to protocol library  
* **Research Integration**:  
  * Monitor scientific research on Ayurveda  
  * When strong evidence emerges, update knowledge base  
  * Example: New study on ashwagandha dosing → Update herb dosage guidelines

**Performance Optimization:**

* **Response Time Improvements**:  
  * Monitor latency metrics  
  * Optimize prompts (shorter prompts \= faster responses without losing quality)  
  * Implement caching for common questions  
  * Upgrade infrastructure if needed  
* **Cost Optimization**:  
  * Monitor AI API costs per user  
  * Optimize prompts to reduce token usage  
  * Use caching to reduce redundant API calls  
  * Use cheaper models (Haiku) for simple tasks where appropriate

**Quarterly Retrospectives:**

* **Team Reviews**:  
  * Engineering, Product, Clinical Advisory Board  
  * Review:  
    * What went well this quarter?  
    * What didn't work?  
    * User feedback themes  
    * Metrics trends (usage, satisfaction, retention)  
    * Upcoming priorities  
  * Output: Prioritized roadmap for next quarter

This comprehensive testing and QA framework ensures AyuAware delivers accurate, safe, effective, and delightful experiences while continuously improving based on real-world use and rigorous validation.

---

**END OF DOCUMENT**

