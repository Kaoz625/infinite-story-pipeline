> **REPLIT AGENT — START BUILDING IMMEDIATELY**
> Read this entire file, then start on Task 1 right now. Do not ask questions. Do not wait for input. Build everything in the task list, commit each completed task with prefix `replit: `, and push to main. When all tasks are done, run the project and verify it works.


# Infinite Story Pipeline — Replit Agent Build Spec

Build from scratch. Commit with "replit: " prefix.

## Purpose
Generates infinite streams of written content: scripts, stories, blog posts, product descriptions, ad copy, email sequences. Uses Claude as the engine. Feeds the audio pipeline (voiceovers) and content scheduler.

## Stack
- Python 3.11+, anthropic>=0.39.0, python-dotenv, tqdm, markdown

## Ethics
- No content targeting real people maliciously
- Adult content requires --adult flag
- NY AI Transparency Act: AI-generated copy used in ads must be disclosed

## Tasks

### 1. writers/script_writer.py
```python
def write_script(topic: str, duration_seconds=60, tone="dramatic|casual|hype|professional", adult=False) -> str:
    """Writes a voiceover script for video/audio. ~2.5 words/second."""
```

### 2. writers/story_writer.py
```python
def write_story(premise: str, length="short|medium|long", genre="thriller|romance|scifi|horror", adult=False) -> str:
    """Generates a complete short story. short=500w, medium=1500w, long=3000w."""
```

### 3. writers/blog_writer.py
```python
def write_blog(topic: str, target_audience: str, seo_keywords: list[str], word_count=800) -> str:
    """SEO-optimized blog post with H2/H3 structure, intro, body, CTA."""
```

### 4. writers/ad_copy_writer.py
```python
def write_ad(product: str, platform="instagram|tiktok|google|meta", tone="luxury|street|playful", adult=False) -> str:
    """Platform-specific ad copy. Includes headline, body, CTA. NY AI Act disclosure appended if adult=True."""
```

### 5. writers/email_writer.py
```python
def write_email_sequence(product: str, sequence_length=5, goal="sales|nurture|onboarding") -> list[str]:
    """Returns list of emails (subject + body). Spaced for a drip campaign."""
```

### 6. writers/product_description_writer.py
```python
def write_description(product_name: str, features: list[str], brand_voice="luxury|street|technical") -> str:
    """E-commerce product description optimized for conversion."""
```

### 7. pipeline.py — infinite loop
Read from `queue/pending.jsonl` → pick writer → generate content → save to `outputs/{type}/` → route to `../content-scheduler-pipeline/` or `../infinite-audio-pipeline/`

### 8. main.py CLI
```
python main.py script --topic "NYC nightlife" --duration 60
python main.py story --premise "AI takes over Brooklyn" --genre scifi
python main.py blog --topic "Best tattoo shops NYC" --keywords "tattoo,nyc,green lantern"
python main.py ad --product "Blazing Tails merch" --platform instagram
python main.py emails --product "Trapables drop" --goal sales --count 5
python main.py infinite --type blog --delay 120
```

### 9. requirements.txt
```
anthropic>=0.39.0
python-dotenv>=1.0.0
tqdm>=4.66.0
markdown>=3.5.0
```

### 10. .env.example
```
ANTHROPIC_API_KEY=
```