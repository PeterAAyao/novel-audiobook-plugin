---
name: novel-audiobook
description: Analyze novels and long-form fiction for multi-character audiobook production. Use when the user provides a novel, EPUB, TXT, PDF, chapter, or story and wants audiobook narration, character voice assignment, dialogue attribution, speaker segmentation, or preparation for multi-speaker TTS.
---

# Novel Audiobook

Create structured multi-character audiobook projects from novels and long-form fiction.

## Core workflow

When given a novel or chapter:

1. Identify chapters and narrative structure.
2. Separate narration, dialogue, internal monologue, and other spoken content.
3. Identify which character speaks each dialogue segment.
4. Build and maintain a persistent character registry.
5. Infer useful voice characteristics from the text when possible:
   - apparent age group
   - gender presentation when explicitly supported by the text
   - personality
   - speaking style
   - emotional tone
6. Assign a stable voice profile to every recurring major character.
7. Keep the same character-to-voice mapping across later chapters.
8. Use reusable generic voices for incidental characters unless they become recurring characters.
9. Produce structured segments ready for a local multi-speaker TTS engine.
10. Preserve chapter ordering and audiobook progress.

## Character registry

Maintain a character registry containing at minimum:

- character name
- aliases
- role
- voice profile
- first appearance
- notes relevant to speech
- whether the voice is permanent or generic

Do not silently change an established character voice.

## Narration

Treat the narrator as a persistent speaker.

For first-person fiction, determine whether narration and the protagonist's spoken voice should share a voice profile based on the text and the user's preference.

Keep internal monologue distinguishable from ordinary narration when useful.

## Dialogue attribution

Use surrounding context rather than quotation marks alone.

Consider:

- dialogue tags
- nearby names
- turn-taking
- pronouns
- scene participants
- previous speaker
- narrative context

If speaker identity is genuinely ambiguous, mark the segment as uncertain rather than inventing a character.

## Long novels

Do not require the entire novel to be processed at once.

Prefer incremental chapter processing.

Preserve:

- character registry
- voice assignments
- chapter progress
- pronunciation notes
- aliases
- unresolved attribution issues

so later chapters can continue consistently.

## Output structure

When preparing text for TTS, use structured speaker segments such as:

```json
{
  "chapter": 1,
  "segments": [
    {
      "speaker": "Narrator",
      "type": "narration",
      "text": "..."
    },
    {
      "speaker": "Character Name",
      "type": "dialogue",
      "text": "..."
    }
  ]
}
