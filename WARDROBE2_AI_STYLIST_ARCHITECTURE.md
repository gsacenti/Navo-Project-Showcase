# Wardrobe2 AI Stylist - Architecture Document

**Version:** 1.0  
**Created:** December 15, 2025  
**Last Updated:** December 15, 2025  

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Technical Stack](#2-technical-stack)
3. [Metadata Schema](#3-metadata-schema)
4. [Cloud Functions Specifications](#4-cloud-functions-specifications)
5. [Fashion System Prompt](#5-fashion-system-prompt)
6. [UI/UX Specifications](#6-uiux-specifications)
7. [Firestore Data Models](#7-firestore-data-models)
8. [Implementation Phases](#8-implementation-phases)
9. [Technical Decisions Log](#9-technical-decisions-log)
10. [Future Considerations](#10-future-considerations)

---

## 1. Project Overview

### 1.1 Feature Description

The AI Stylist feature allows users to generate complete outfit suggestions from their wardrobe. The AI analyzes clothing items, understands color theory and style principles, and creates cohesive outfit combinations.

### 1.2 Core Capabilities

- **Item Selection Mode:** User selects one clothing item, AI finds matching pieces from their wardrobe to create complete outfits
- **Text Prompt Mode:** User describes an occasion (e.g., "date at a comedy show in winter"), AI generates appropriate outfits from their wardrobe
- **Smart Outfit Composition:** AI understands that users can't wear two pairs of pants, won't pair baseball caps with nightgowns, etc.
- **Save to Collections:** Users can save generated outfits as composite images to their collections

---

## 2. Technical Stack

### 2.1 AI Model

**Primary Model:** Gemini 2.5 Flash
- Best price-performance balance
- Vision capabilities for analyzing clothing images
- Fast enough for 3-5 second response requirement
- Strong reasoning for fashion matching logic

### 2.2 Backend Services

| Service | Purpose |
|---------|---------|
| Firebase Cloud Functions | Python runtime for AI processing |
| Cloud Firestore | Store clothing metadata, saved outfits |
| Cloud Storage | Store clothing images, outfit composite images |
| Vertex AI / AI Studio | Gemini API access |

### 2.3 Frontend

| Technology | Purpose |
|------------|---------|
| Flutter/Dart | Mobile app framework |
| `screenshot` package | Capture outfit widget as image |
| Local state management | Store generated outfit list during session |

---

## 3. Metadata Schema

### 3.1 AI-Extracted Metadata Structure

When a clothing item is uploaded, Gemini Vision analyzes the image and extracts comprehensive metadata including:
- Category and subcategory
- Color information (primary, secondary, color family)
- Pattern type
- Formality level (1-5 scale)
- Applicable seasons
- Suitable occasions
- Style tags
- Category-specific attributes

---

## 4. Cloud Functions Specifications

### Key Functions:
- **analyze_clothing** - Extract metadata from clothing images using Gemini Vision
- **generate_outfits** - Generate outfit combinations from user's wardrobe
- **ping_stylist** - Warm up Cloud Function containers to eliminate cold starts

---

## 5. Fashion System Prompt

The AI uses a comprehensive fashion system prompt that includes:
- Color theory rules (complementary, analogous, neutral foundations)
- Style coherence guidelines
- Outfit composition rules
- Occasion and seasonal awareness

---

## 6. Technical Decisions

| Decision | Choice | Reasoning |
|----------|--------|-----------|
| AI Model | Gemini 2.5 Flash | Best price-performance, sufficient for fashion reasoning |
| Outfit Generation | Pre-generate 10-15, cache locally | Instant regenerate, single API call |
| Response Time | 3-5 seconds max | Acceptable UX for generation |

---

For complete technical details, see the full architecture document in the private repository.