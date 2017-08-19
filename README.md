# Thoth

I've had a idea for a text grammar etc. type checker, that's node based a little like a shader graph program.

The text would be read glyph by glyph by a ReaderNode.
A WordNode would listen to the ReaderNode and build up words.
Then maybe a SentenceReader etc.
The a SpellChecker might listen to the WordNode and report errors through that.
Everything is pumped by the GyphReader and new rules can be created by combining nodes.

This structure is supposed to make it efficient and easy to extend.

## Word Reader

- OnRecognise(word:string, start:Pos, end:Pos)
- Listener : CharReader

Pos here would be line number and column number.

## Determinators

In English determinators is word for a `a` or `an`. There's general rule about when to use each. `a` is used before a word starting a vowel and `an` before a constant. So you might want a checker to inform this rule (possible with some exceptions).

you need something like

bool prevDeterminator = prevWordNode.exists && prevWordNode.isDeterminator

> if the previous word is `a` and then current word starts with a `constant` and it's not in exceptions, then that's probably an error.

but it shouldn't be an active check, it should be a passively driven by the Gylph reader.
