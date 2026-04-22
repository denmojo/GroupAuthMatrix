# GroupAuthMatrix
A single-file HTML page that generates printable authentication cards for a group, one per member.

You enter the number of people (with optional custom names, defaulting to NATO phonetic) and a code length, and the page builds an individualized card for each member showing only the codes they need: one code to prove themselves to every other member, and one to verify every other member back. The shared directional secret across any ordered pair means Alpha's "prove to Bravo" code matches Bravo's "verify Alpha" code, and nobody's card leaks codes from pairs they're not part of.

Codes come from crypto.getRandomValues over a 32-character alphabet with ambiguous glyphs removed (no 0/O, no 1/I). Cards are pinned to 5" × 3" landscape index-card dimensions with 1cm gutters so a printout can be cut apart cleanly.

Capacity under the 3" × 5" constraint:
- 1 side per member: up to 11 members
- 2 sides per member: up to 21 members
- Beyond 21 it keeps going (Side 3, Side 4...) up to an input cap of 50

The practical maximum for a double-sided card is 21 group members.

"Code sets per member" (min 1, max 10). Each set gets its own independent random matrix of codes, and cards are labeled Member Alpha's Card #1, Card #2, etc., with (Side 1 of 2) appended when a card overflows. Output is grouped by member then by set, so each person's stack stays contiguous for distribution. At authentication time, the requester says "Authenticate 3" and everyone pulls Card #3.

To prevent code collision, length-2 codes are fine for 4–6 members and mostly ceremonial. For groups of 8+, bump the code length field to 3. For 15+, use 4. A coincidental duplicate doesn't break security (an attacker still can't see other cards), but it can produce ambiguous challenges at the moment of authentication, which is the real cost.

No dependencies, no build step, no network calls. Open the file, generate, print.
