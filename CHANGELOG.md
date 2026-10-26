# Scan Master Changelog

All notable changes to this project are documented here.
Dates use ISO 8601 (YYYY-MM-DD).

---

## [2.28.1] - 2026-10-26

### Fixed

- **Equations in Word documents, checked in Word itself.** Eleven varied equations (fractions, roots, sums, integrals, matrices, accents, limits, scripts) were saved by ScanMaster and opened in Word, which read every one as a real Word equation of the right kind. That check found three faults, now fixed: an **overline** (`\overline{AB}`) was stored with an underline character, so it drew and was spoken as an underline; it is now an overline, and Word gets a real overbar (and underbar) instead of a loose character; and a **brace over or under** an expression is now Word's own group character rather than an accent with a stray symbol.

---

## [2.28.0] - 2026-10-26

### Fixed

- **Explore Equation could not be used properly.** It started on the whole equation, where Left and Right only said "end of math", and it refused to start when the cursor was just after the equation (where it is after Insert Equation, or after arrowing through one). Now it says the whole equation, then puts you on its first part so Left and Right move between the parts at once, and it works from the end of an equation too. The announcement lists the keys.

### Changed

- **Equations are stored as proper MathML in Scan Master documents.** A `.smdx` file used to keep an equation as escaped text inside an attribute; it is now a real `<math>` element in the MathML namespace inside the run (other tools can read it, and it is far more compact). Older files still open. Word documents already store equations as Office Math (OMML), and HTML and EPUB as MathML.

---

## [2.27.9] - 2026-10-23

### Fixed

- **Dialogs cut off their text on a screen scaled above 100%.** On a 150% screen the Check for Updates window hid its first line behind the release notes, and its controls were too small for their words. Every window was laid out for 100% while its text was drawn at the screen's scale. Now every control's size and position, and each window's margin, are scaled to the screen's setting as the window is made (at 100% nothing changes). This covers all dialogs, including Find, Header and Footer and Preferences. I could only test it at 100%, so please tell me about any window that still looks wrong at 125% or 150%.

---

## [2.27.8] - 2026-10-23

### Removed

- **File > Export As is gone.** It did what Save As does (the same window, the same formats); the only difference was that the open document stayed on its original file. To keep a copy, save the document under another name with Save As. The Keyboard Manager no longer lists it, and Help says so.

---

## [2.27.7] - 2026-10-23

### Fixed

- **Menu bar cut off on a screen scaled to 150%.** The words of the menu bar (File, Edit, View...) were cut off at the bottom and right, and the toolbars sat over them. The cause: the program did not tell Windows how it handles screen scaling until its editor started, so the menu bar was made while Windows still treated the program as unscaled, and measured it for 100% (19 pixels high, where 150% needs 29). The program now says it is scaling-aware first thing, before any menu or window exists, and the log records it (a "[Frame] at start the program was DPI-unaware" line). Nothing changes at 100%.

---

## [2.27.6] - 2026-10-23

### Fixed

- **Tables are now read in Save as Audio.** A table was skipped when a document was saved as an audio file, so a book's table of contents (which many books hold as a table, such as the Project Gutenberg book `pg50400-images-3.smdx`) was missing from the recording. Each row is now read as one sentence, with a comma between the cells (for example "CHAPTER ONE, Wings of the Brave."), in every format and split mode. Talking books already did this. The Help topic Speech and Navigation says so.

---

## [2.27.5] - 2026-10-22

### Changed

- **The old account name is gone from the program and its files.** The changelog (which is built into the program and shown in Release Notes), the NVDA add-on's source and the project's documents no longer carry the previous GitHub account name; the author is Deenadayalan Moodley throughout.

---

## [2.27.4] - 2026-10-22

### Changed

- **ScanMaster now lives on a new GitHub account.** The project's repositories moved to a new GitHub account, `DeenadayalanMoodley` (`DeenadayalanMoodley/ScanMaster-releases` holds the releases and the issues). The update check, the release-notes refresh, the downloads of the optional voice and Docling add-ons, Help > Report a Bug and the web addresses in the installer and the About box now use the new address directly. Copies installed before this version keep updating through GitHub's redirect, so they will find this release. Also fixed: Release Notes > Refresh from GitHub always came back empty, because the changelog was never published where it looks (the releases repository held only a README); the changelog is now published there with every release.

---

## [2.27.3] - 2026-10-22

### Added

- **Find in reverse.** The Find and Find and Replace windows have a **Find Previous** button, which searches backwards from the start of the current selection and wraps round to the end of the document (with regular expressions too). **Edit > Find Next** (Ctrl+Alt+F) and **Edit > Find Previous** (Ctrl+Alt+Shift+F) repeat the last search without the window and have the screen reader read the text they land on, or say it was not found. (F3 stays Pause/Resume for speech; the shortcuts can be changed in the Keyboard Manager.) "Replace with" now has the access key Alt+H, as Alt+P is Find Previous.

---

## [2.27.2] - 2026-10-22

### Changed

- **Find (Ctrl+F) is now only a Find window.** It used to show the replacement text and the Replace and Replace All buttons as well. It now has just the text to find, Match case, Whole word, Use regular expression, and Find Next (Enter presses it); Find and Replace (Ctrl+H) still has the replacement text and the Replace buttons. A pattern that is not a valid regular expression is now reported as such, with the reason ("unclosed group", say), instead of "not found". The labels have access keys (Alt+N for the text, Alt+M, Alt+W, Alt+X).

---

## [2.27.1] - 2026-10-22

### Fixed

- **Save as Audio failed with "ffmpeg did not complete within the timeout."** The encoder was given a fixed five minutes. It is now judged by progress instead: it is stopped only if the audio file stops growing for ten minutes (or after 24 hours in all), however long the book is. What ffmpeg says is also read while it runs, so a full message pipe cannot stop it. If an encode is still given up on, the message says how long the file went without growing, and the log (AudioExport) records the ffmpeg arguments so the cause can be found; please send that line with a bug report (Help > Report a Bug).

---

## [2.27.0] - 2026-10-22

### Added

- **Help > Report a Bug or Suggest a Feature…** A form (type of report, short summary, what happened, steps to reproduce, what you expected) that becomes an issue on GitHub (`DeenadayalanMoodley/ScanMaster-releases`), labelled bug, enhancement or question, so reports are tracked. System information (ScanMaster and Windows version, screen reader, speech engine, update channel) is added by default and shown in a box first; the end of the log can be added too (off by default, with your user name hidden). **Submit to GitHub** opens GitHub in the browser with the report filled in (and copied to the clipboard), or, if you give a GitHub access token, makes the issue itself and opens it; the token is kept protected on this computer only if you ask, and only after it has worked. **Copy to clipboard** copies the report without sending it.

---

## [2.26.1] - 2026-10-21

### Fixed

- **The Styles list did not show which style the cursor is in, and a character style's extent was unknown.** Apply Style (Ctrl+Shift+S) and Styles… now open with the style at the cursor selected in the list: the character style the cursor is in (Speaker 3, say) or else the paragraph's style. When the cursor is in a character style, its whole stretch is also selected and read out (its name, how many characters, and its first and last words), so what Apply changes is exactly that stretch, and you know where it starts and ends.

### Changed

- **The ScanMaster.exe launcher now carries version information and a manifest** (name, company, version, "run as the current user"). It had none, and Windows Defender's machine-learning check wrongly called the bare launcher a trojan (Trojan:Win32/Bearfoos.A!ml). If Defender still reports ScanMaster.exe, it is that same false alarm: choose Allow, or send the file to Microsoft at https://www.microsoft.com/wdsi/filesubmission.

### Added

- **Format > Character Style > Select This Stretch** selects the whole stretch of the character style the cursor is in and says what it is, without opening a dialog (it can be given a shortcut in the Keyboard Manager).

---

## [2.26.0] - 2026-10-21

### Added

- **Pan each voice between the left and right speakers.** Speech Settings has a new *Pan (left to right)* slider for the profile's voice (the narrator) on the Voice section and for each document element (Speaker 1-4, headings, your own styles) on the Document Elements section, from Left 100% through Centre to Right 100% in steps of 10%. The position is heard when the document is read aloud (each voice in its own place, with any engine) and in Save as Audio, which is made in stereo when any voice is off-centre and stays mono otherwise. The element list shows each element's pan. The values beside the Rate, Volume, Pitch and Pan sliders now follow the sliders as they are moved (they only showed the saved value before).

---

## [2.25.0] - 2026-10-21

### Added

- **Library: the Internet Archive, and libraries of your own.** The Library window now has a second built-in library, the Internet Archive: ready-made lists (Popular, Latest, Project Gutenberg copies, American libraries, 23 subjects, 6 languages), a search of titles, authors and subjects, the item's description, and download or preview of the text (scans are saved as plain text tidied into paragraphs; small EPUBs as EPUB; borrow-only books and huge page-picture EPUBs are not offered). **Add library** takes the address of any OPDS catalogue (a Calibre server, Feedbooks, a public library) with an optional user name and password, learns how to search it from its first page, and lists it in the Library box; **Sign in** corrects the sign-in and **Remove library** takes it off. Passwords are kept protected on this computer and sent only to the library's own site, and are refused for plain `http://` addresses. Bookshare is still not included (it needs a partner key from Bookshare). The *Online Library* help page covers it.

---

## [2.24.0] - 2026-10-20

### Added

- **File > Library: find, read about, preview and download books from an online library.** The first library is Project Gutenberg (no account needed). *Browse and search online libraries…* has a Category box (Popular, Latest, Random, the library's home page, 23 subjects and 18 languages), a Search box, a list of books and categories (Enter on a category opens it; Back and Next page move through results), and a Description box with the library's summary, author, subjects and formats. **Preview** opens the first part of the book as an unsaved tab; **Read** downloads it into the library folder and opens it; **Download** only saves it (as `Author\Title.epub`, with a progress report, Stop to cancel, and a half-finished file never left behind); **Library folder** opens the folder. *Choose library folder…* and *Open library folder* are in the same submenu. Built on a general OPDS catalogue reader, so more libraries (Standard Ebooks, Internet Archive, any OPDS address) can be added next; signing in and Bookshare (which needs a partner key from Bookshare) are not in yet. A new help page, *Online Library*, explains it.

---

## [2.23.9] - 2026-10-20

### Fixed

- **Saving as audio failed with "Speak failed: Invalid HTTP status. (0x80004005)".** With an online (natural) voice, the voice's web service sometimes answers a request with an error, more often when several parts are rendered at once. A part that fails that way, or with "Timer Expired", a timeout or a lost connection, is now tried again after 3, 8 and 20 seconds before the export gives up. Each retry is written to the log (AudioExport).

---

## [2.23.8] - 2026-10-20

### Fixed

- **Detect Speakers lost the second half of a speech split by a tag.** For `"You've heard of him, sir?" Dave asked quickly. "Farmer thought the name familiar."` the model often named the first part and missed or mislabelled the second. Two quotations in one paragraph with only a short tag between them are now one speaker's speech: the second takes the first's speaker (and a first part the model left unnamed takes the second's). It is not applied when the second quotation has a tag of its own (`"Hello," said Bo.`), nor across a new paragraph or several sentences of narration. The instructions to the model say the same.

---

## [2.23.7] - 2026-10-19

### Fixed

- **Detect Speakers gave up on a passing service fault.** A busy or overloaded service (HTTP 429, 500, 502-504, Cloudflare's 520-524) or a lost connection is now tried again after 2, 6 and 15 seconds before the passage is counted as failed, so one hiccup at the start no longer ends the whole run. When it does fail, the message says what to do: a model too big for the computer's memory (an Ollama "failed to allocate buffer" error) points to choosing a smaller or cloud model for Speakers in Preferences > AI Tasks.

---

## [2.23.6] - 2026-10-18

### Fixed

- **Changing the language in the spelling dialog crashed the program.** The language box kept each row's tag in a way that read memory it did not own (and freed it on the first read). The tags are now kept in a list by row, in the box's sorted order.

---

## [2.23.5] - 2026-10-18

### Fixed

- **Detect Speakers missed some quotations and gave some the wrong speaker.** Dialogue in single curly quotation marks (the British style) was not found at all; it is now, when the passage uses no double marks (apostrophes such as don't are not mistaken for quotation marks). Each passage is now sent with the end of the text before it, so a conversation that runs across the cut is followed, and the instructions say in which order to weigh the clues (the tag next to the quotation first, then who is addressed, then alternation).

---

## [2.23.4] - 2026-10-17

### Fixed

- **The spelling dialog's Context box no longer traps the Tab key.** Now that it is editable it kept Tab for itself; Tab and Shift+Tab move to the next and previous control again.

---

## [2.23.3] - 2026-10-17

### Fixed

- **EPUB (and HTML) books no longer run words together.** A book's text is hard-wrapped in its source ("that
goes"); a line break in the source is white space, as in a browser, but it was kept as a break inside the paragraph, which showed as "thatgoes". Source white space is now one space; real `<br>` breaks and `<pre>` text are kept, and saving to HTML/EPUB writes `<br/>` for a line break so it survives a round trip. On a real 1,176-paragraph book, paragraphs with a stray break went from 1,014 to 25 (real breaks).
- **A crash when an edit was made while a screen reader or other UI Automation client was attached.** A text-change message could arrive while the tab list was in use and end the program. The tab list is no longer held while the editor is called, and the handler no longer panics. A crash now also leaves its reason in `panic.log` beside the log.

### Added

- **The spelling dialog's Not in dictionary and Context boxes can be edited.** Put the missing space into the Context box and press Change; only the changed part is replaced (formatting elsewhere stays) and Undo change restores it. Typing over the flagged word works too. Undo now resumes at the start of the word.

---

## [2.23.2] - 2026-10-17

### Added

- **A way to try another DPI mode on a scaled screen (for the cut-off menu bar).** A log from a 150% screen showed the menu bar 19 pixels tall (the 100% height) while the window was at 144 DPI and Windows' own menu height at that scaling is 30: Windows is measuring the bar for 100% text. To find out whether the DPI mode is the cause, set the environment variable `SCANMASTER_DPI_MODE` to `system` (or `unaware`, or `permonitor` for the normal mode) before starting Scan Master, for example in a command prompt: `set SCANMASTER_DPI_MODE=system` and then run `ScanMaster.exe` from that same prompt. It writes a warning line to the log saying which mode it started in. Nothing changes unless you set it. If `system` mode shows the menu bar properly, tell me and it can become the setting for scaled screens.
- The `[Frame]` log line now also says the DPI mode of the window and of the thread running it.

## [2.23.1] - 2026-10-17

### Fixed

- **Menu bar cut off on a scaled (150%) screen, in the light theme as well.** On such a screen Windows sometimes measures the menu bar for smaller text than it then paints, so the words are cut off at the right and the toolbars sit over the bar's lower half. Scan Master now checks, whenever the window is maximized, restored or moved to a screen with other scaling (and when it starts), that the bar is as tall as its text needs at the window's scaling and that no item is narrower than its words. If not, it writes the numbers to the log as a warning (at any log setting; look for `[Frame]` lines) and has Windows measure the menu again, in the window's own DPI mode. Checked here at 100%: no false alarm, and the repair (forced on) leaves the menu with all its items and the window unchanged through maximize and restore. **Not yet confirmed on a 150% screen** (this computer isn't scaled): if the bar is still cut off, the `[Frame]` warning in `scanmaster.log` says what Windows measured and whether measuring again helped. (`SCANMASTER_FORCE_MENU_REPAIR=1` makes it measure again every time, a test aid.)

## [2.23.0] - 2026-10-17

### Added

- **Detect Speakers with AI (Tools › Detect Speakers with AI…).** For audiobooks: the AI reads the document (or the selection), works out who says each line of dialogue, and puts a Speaker style on those words, leaving the narration alone. The window lists the characters it found, each with its number of lines and the style it will get (most lines get Speaker 1, then 2, and so on). For each character you can pick another style, *No style*, or say it is the **same character as** another (a model sometimes lists "Mr Smith" and "John Smith" apart). **Apply Styles** puts them all on in one step, so **one Undo** takes every style off again. With more than four characters, Speaker 5, Speaker 6 and so on are made for you; give each style its own voice in Speech Settings. Quotation marks are found by Scan Master itself, which numbers each quotation and asks the model only who speaks it, so even a small local model can't garble the words and every quotation gets an answer; dialogue written as a script (`NAME: words`) or with dashes is found by the model instead. The document is read a part at a time with progress and **Stop**; if the document changes while it is working, nothing is applied. After applying, the editor is read back to confirm that every line holds its style. The provider and model are chosen in **Tools › Preferences › AI Tasks › Speaker detection**. Checked live with a local Ollama model (`llama3.1:8b`): a three-character story (all seven quotations attributed correctly, all applied, one Undo removed all) and a five-character story (Speaker 5 created). The model can still be wrong when a speaker is never named, so check the characters before applying. See the help ("Detect speakers").
- The editor can now apply character styles to many stretches of text in a single undo step without moving the caret (used by the above).

## [2.22.17] - 2026-10-16

### Fixed

- **Dark menu bar still cut off and running together on a scaled (150%) screen.** The dark menu bar is painted by Scan Master, and on a scaled screen Windows measured the bar and its items for smaller text than was drawn, so the words touched each other and were clipped at the top and bottom. The bar now measures each item with the same font it draws with (plus a little space each side), and the font is kept to what the bar can hold. Checked by drawing the text 50% larger than Windows measured: the words stay apart and inside the bar, and at normal size nothing changes. (`SCANMASTER_MENU_FONT_PERCENT` scales the menu font, for testing.)

## [2.22.16] - 2026-10-15

### Fixed

- **JAWS read the line you had just typed when you pressed Enter, and mishandled blank lines.** JAWS asks the editor for the paragraph (or word) at the caret. On an empty line the editor answered with the previous line's text and its line break, so after Enter you heard the line you had just left instead of "blank", and arrowing onto a blank line did the same. Only the line unit was right. Now an empty line is empty for the word and paragraph units too (just its line break, or nothing at the end of the document), and a paragraph ends at its own line break instead of running on through the blank lines after it ("text, blank"). Checked by asking the editor's UI Automation text for the caret's character, word, line and paragraph after typing and pressing Enter, before and after; `scripts\uia-text-probe.ps1` repeats that check. Not yet heard with JAWS itself. Setting the environment variable `SCANMASTER_OLD_BLANK_UNITS` restores the previous answers.

## [2.22.15] - 2026-10-15

From the code audit (`rust/SCANMASTER_RUST_AUDIT.md`).

### Changed

- **Network scanner certificates (F18).** A network scanner using https with a self-signed certificate used to be accepted whatever certificate it showed, so anyone on the network could pose as it. Now the first connection asks whether to trust the scanner and shows its certificate fingerprint; Scan Master remembers it and accepts only that certificate for that scanner. A certificate that changes is refused, with the old and new fingerprints shown. The handshake's signature is checked as well, so a copied certificate does not pass. Plain http scanners are unchanged. Checked with a fake https scanner: first contact refused, trusted scanner connects, changed certificate refused, trust is per address and port. See the new help section "Trusting a network scanner".
- **Results from background jobs are no longer overwritten (audit section 5.1).** Saves, message boxes from background work, opened documents, imports, language pack installs and grammar checks each handed their result over in a single slot, so a second result that arrived before the window had read the first replaced it and the first was lost. Each result now waits in order. A check for updates started by choosing another update channel replaces the earlier check, and a late answer from the earlier one is ignored.

### Fixed

- After a failed check for updates started from the update window, the window no longer stays on "Looking for ... releases" with OK greyed out.

## [2.22.14] - 2026-10-15

### Added

- **Update channels.** The Check for updates window has radio buttons for **Stable releases**, **Release candidates** and **Beta releases**, so one updater serves every kind of build. Each channel includes the more stable ones before it (a release candidate outranks a beta of the same version, and the final release outranks both). Choosing a channel looks again at once and is remembered; a beta build starts on Beta, everything else on Stable. The window now opens when you are up to date too (it used to be a message box), so the channel can be changed from it. The channel of a release comes from its tag (`-rc.N`, `-beta.N`), not from GitHub's prerelease flag.

## [2.22.13] - 2026-10-15

### Fixed

- **The updater refused every signed update.** It handed the release's tag (`v2.22.12`) to the signature check, but releases are signed under the bare version (`2.22.12`), so a real update always failed with "the update's signature does not match the file" (2.22.9 itself was not checked). The check now drops the `v`. Installs of 2.22.9 to 2.22.12 cannot update themselves once: install this version by hand (the setup program, or unzip the portable zip over the folder); updates after that work. The update download also no longer gives up after 10 minutes (it can take longer on a slow connection).
- **Menu bar words running into each other in dark mode** (File Edit ViewInsertFormat PagesSpeech...). The dark menu bar is painted by Scan Master itself, and it drew the words in the plain system font, which is bigger than the font Windows had measured the menu items for, so each word spilled into its neighbours. It now draws with the menu font from your Windows settings, scaled for the screen's DPI, so the words fit their spaces.

## [2.22.12] - 2026-10-15

Maintenance release from the code audit (`rust/SCANMASTER_RUST_AUDIT.md`).

### Changed

- **Help:** the privacy notes now say not to send the settings database or a portable folder in a bug report (it holds your API keys), and that recovery copies of unsaved documents are plain, unencrypted files that are removed on save, close, or when the setting is turned off.
- Removed two source files that were no longer used and fixed comments that still described them. No change to how the program behaves.

## [2.22.11] - 2026-10-15

From the code audit (`rust/SCANMASTER_RUST_AUDIT.md`).

### Added

- **Recovery copies are a setting.** Preferences > Advanced has **Keep recovery copies of unsaved work** (on by default); turning it off also removes the copies already kept. **Never save a PDF without tags** is there too.
- **Scan both sides (feeder)** in Preferences > Scanning.

### Fixed

- **Feeder scanning.** The feeder and two-sided scanning used to be one choice, and a scanner asked for the feeder could still scan the glass. They are now separate: Multi-Page (ADF) mode uses the feeder, and two sides only if you ask. For network (eSCL) scanners the whole stack of sheets is one job, so pages after the first are no longer lost; the job is always removed afterwards. For WIA scanners the feeder or flat glass is now selected on the device, and an empty feeder says so.
- **Network scanner protocol.** Requests follow the eSCL specification (ScanSettings, the job address from the scanner's reply, `Feeder` as the source), a reply pointing at another host is refused, and a busy or not-ready scanner gets a clear message.

## [2.22.10] - 2026-10-15

From the code audit (`rust/SCANMASTER_RUST_AUDIT.md`).

### Added

- **Recovery copies of unsaved work.** Autosave only ever saved the open tab, and only if it already had a file name, so a crash lost unnamed documents and everything in other tabs. Scan Master now keeps a copy of every document with unsaved changes (named or not, in any tab) in `recovery` in its data folder, about once a minute and only when the text changed (a very large document backs the next copy off). The copy goes when the document is saved or closed, or Scan Master closes normally. After a crash or power cut, the next start asks whether to open what was kept (**Yes**), throw it away (**No**) or ask again next time (**Cancel**); documents open as **Recovered - name** tabs marked as unsaved, not saved over the original file. Checked by typing into a new document, ending the program without warning, and starting it again: the question appears and the text comes back. The copies are not encrypted; the setting `prefs.recovery_copies` (default on) turns them off. This is separate from, and does not need, the Autosave setting.

## [2.22.9] - 2026-10-15

From the code audit (`rust/SCANMASTER_RUST_AUDIT.md`): updates are now proved to come from the release maker, and a failed update puts the whole install back.

### Changed

- **Updates are signed.** Each release's setup program and portable zip carry a signature (a `.sig` file beside them on the release page), made with a key that only the release maker holds; ScanMaster carries the matching public key. Before it runs a downloaded update it checks that signature, so a replaced file on the release page, or a changed release, is refused with a message rather than run. The update helper checks the file's SHA-256 again just before it uses it. This applies from this version on: **this version's own update is not checked** (the program that downloads it is the older one), and every later release must be signed or it will be refused.

### Fixed

- **A failed portable update could leave a mix of old and new files.** Only the `app` folder was put back. The update is now checked first (a valid zip, only safe file names, a launcher, an app and a helper in it), unpacked completely into a staging folder, and only then swapped in, file by file, with each replaced file kept in a backup folder. Any failure puts every file back, including those outside `app`. The previous version is kept until the new one has been seen to start: if it ends with an error within 15 seconds, the previous version is put back and started.
- **An update could report success and leave nothing to start.** A zip that lacked the program used to unpack, delete the old copy, and fail on the restart.
- **The update instructions were trusted completely.** The program to restart must now be inside the install folder, a process id that does not fit is refused instead of being cut down, and the file named in the instructions must still be the one that was checked.

## [2.22.8] - 2026-10-14

From the code audit (`rust/SCANMASTER_RUST_AUDIT.md`): a damaged or hostile file can no longer use up all the memory or overflow the stack.

### Fixed

- **A small file could expand to gigabytes.** Reading a `.smdx`, `.docx`, `.epub`, `.smf` or a web-page `.zip` now counts the bytes actually unpacked: an entry over 256 MB, an archive over 2 GB in total, or an archive with over 100,000 entries is refused with a message instead of filling memory.
- **A file nested thousands of levels deep could crash the program.** XML and HTML nested more than 512 levels deep is refused (an HTML page then opens as plain text blocks).
- **A Kindle book could claim a huge size.** Room for a book's text was reserved from the length its header claims, so a tiny file claiming 4 GB reserved 4 GB; the room now follows what is really in the file, and a book that unpacks to over 512 MB is refused.
- **A scanner could send an endless answer.** Scanner replies are read up to 16 MB for text and 512 MB for a scanned page.

## [2.22.7] - 2026-10-14

More from the code audit (`rust/SCANMASTER_RUST_AUDIT.md`): content from other people's files can no longer put active content into what you export, and EPUB export keeps pictures.

### Fixed

- **An equation could carry a script into an exported page.** Equations are written as MathML exactly as stored, so one that ended `</math><script>...` put that script into the HTML or EPUB. An equation is now read as XML and written back with only the MathML elements and attributes that equations use; one that is anything else is written as its plain text.
- **A heading font name could end the page's stylesheet.** Font names are cut down to letters, digits, spaces, `-`, `_` and `.`; text colours must be a plain colour (`#rrggbb`, a name, or `rgb(...)`).
- **Links could be `javascript:` or `file:` addresses.** Exports now write only web, mail, phone, relative and in-page links (other links keep their words, without the link), and a link in the editor opens only if it is a web, mail or phone address.
- **A web page could pull in other files from your computer as pictures.** Opening an HTML file now takes a picture only from the page's own folder (no absolute or network path, no `..`), only if it is really a picture, and not over 64 MB.
- **EPUB export lost every picture.** Pictures are now put in the book with their alternative text (a picture whose bytes can't be found is written as "[Image: description]"), and read back as pictures.

## [2.22.6] - 2026-10-14

From an audit of the Rust code (`rust/SCANMASTER_RUST_AUDIT.md`); each fix below was confirmed in the code first.

### Fixed

- **Saving could damage the document it was saving over.** A file is now written to a temporary file next to it, flushed to disk, and then moved over the old one, so a full disk or a crash leaves the previous version intact. If "Back up on save" is on and the backup can't be made, the save stops with a message instead of carrying on without it. Clips are written the same way.
- **A slow save could change the wrong tab.** Saving runs in the background; if you switched to another tab before it finished, the other tab took on the saved document's file name and was marked saved. A save now belongs to the tab it was made in, and that tab is only marked saved if you didn't type after the text that was saved.
- **"Save" in the "save before closing?" question called the close off.** The save runs in the background, so the document still looked unsaved and the window stayed open. It now waits for the save to finish.
- **Removing one Piper voice removed all of them.** Only the chosen voice's files are removed now.
- **Moving a page lost anything that wasn't text.** Pages > Move Page Up/Down and Reorder Pages rewrote the page's text, losing pictures, tables and formatting. The two pages are now exchanged whole.
- **A failed update step could delete the launcher's file.** The launcher now moves the old file aside first and puts it back if the new one can't be moved into place.
- **Preferences > AI Tasks "Refresh models" did nothing.** Its finished message shared a number with the account check's, so it was never handled.
- **The build without the Qt editor failed to compile.**

## [2.22.5] - 2026-10-14

### Fixed

- **Menu bar still cut in half after maximizing at 150% scaling.** Version
  2.22.4 put the toolbars right but the menu bar stayed too short for its
  words. The program did not handle Windows' message that the window's
  display scaling changed (the window moved to a monitor with other scaling,
  or the scaling changed), which is what makes Windows measure the title bar
  and menu bar for the new scaling; it now takes the rectangle Windows
  suggests. Not reproducible at 100% scaling, so this is untested at 150%.
- **Diagnostics for it.** The log (`scanmaster.log`) now has `[Frame]` lines
  after start-up, a maximize or restore and a scaling change: the window's
  and the system's DPI, and the menu bar's position and height. If the menu
  is still cut off, send those lines.

## [2.22.4] - 2026-10-14

### Fixed

- **After maximizing, the menu bar was cut in half and a toolbar was
  hidden.** Seen at 150% display scaling: only the top half of File, Edit,
  View and the rest showed, with the Formatting toolbar directly under them.
  Two causes. The Formatting toolbar moved itself to the top of the window
  whenever the window was resized, so it sat on top of the Standard toolbar;
  the toolbars are now placed only by the program. And Windows could measure
  the menu bar for the wrong size after a maximize or restore; the frame is
  now measured again, once per change of state. The first cause was found and
  checked at 100% scaling (maximize, restore, maximize: both toolbars stay in
  place). The menu measuring could not be reproduced at 100%, so tell us if
  the menu is still cut off after updating.

## [2.22.3] - 2026-10-13

### Fixed

- **Describe All Images could report every image done and set none.** Each
  description is matched to its image by the image's bytes, and the editor
  gives an image's bytes back in another encoding once it has drawn the
  picture, so the match failed. When no image has been added or removed
  during the run, a description now goes to the image at its original
  position. The progress line also counted failed images as described; it
  now counts only the ones described and says how many failed.
- **Narrator saw a wrapped paragraph as one long line.** Asked which line
  the caret is on, the editor gave the wrapped line, but when a screen
  reader stepped to the next or previous line it stepped by whole
  paragraphs, so the two answers disagreed. Both now use the wrapped lines
  (step 10 of `patch_qt_scanmaster.py`).
- **Scrolling a range into view moved the caret.** Qt's UI Automation
  `ScrollIntoView` put the real caret at the range; Narrator calls it as
  you type. It now only scrolls (step 11).
- **Narrator's select right after typing threw the caret to the start.** A
  select that arrives within 0.7 seconds of a text change is ignored
  (step 12).

## [2.22.2] - 2026-10-12

### Fixed

- **Narrator threw the caret back after the first typed letter.** Typing
  "This is a test" with Narrator running gave "his is a testT": Narrator
  keeps the text position it took while the document was empty and
  selects it after the first letter, so the rest of the line went in front
  of that letter. The editor now ignores a select request on a text
  position made before the text last changed (step 9 of
  `patch_qt_scanmaster.py`). Reproduced with a script that does what
  Narrator does: the old build scrambled the line every time, the new one
  types it correctly.
- **The paragraph unit was the whole document.** For screen readers that
  ask for the current paragraph (Narrator does), the second line of a
  document came back together with the first. A paragraph now ends at a
  line break or a table cell boundary (step 8).

## [2.22.1] - 2026-10-11

### Fixed

- **Narrator and JAWS could not see the editor.** The editor was reported
  to UI Automation as a window called "ScanMaster", and to MSAA as a plain
  window, so Narrator said only "Document window" and JAWS (which first
  asks for the MSAA role) found no text. It is now an *edit* named
  "Document": UI Automation reports an Edit control (Qt's UIA plugin
  patched, step 7 of `patch_qt_scanmaster.py`), and the window answers MSAA
  as a text box, which is what JAWS' own "UIA Edits" rule looks for before
  it reads the text through UI Automation. Checked by recording speech
  and reading NVDA's log, old build against new: Narrator said "Document
  window" and now says "Document, Edit" and reads the characters as the
  caret moves; JAWS read nothing of the text and now says "document
  edit", echoes typing, reads the line on Enter, Up and Down, and the
  characters on Left; NVDA reads typing, Enter and lines exactly as
  before, and now hears "Document, edit" instead of "Document window"
  on entering the editor.
  `SCANMASTER_UIA_WINDOW=1` and `SCANMASTER_MSAA_OFF=1` (environment
  variables) bring back the old answers, for comparing screen readers.

### Changed

- **AI Tasks offers only models that suit each job.** Image descriptions
  and OCR list only models that can read pictures; proofreading, layout,
  grammar, the AI Assistant and the dictionary list chat models (no
  embedding, speech, drawing or OCR-only models). Ollama, OpenRouter and
  Mistral are asked what each model can do; for other providers the name
  is read. If a provider's models can't be told apart, the whole list is
  shown. Choosing a model without vision for an image job also now gives
  a clear message naming the installed models that can read images,
  instead of Ollama's "Multimodal data provided" error.

## [2.22.0] - 2026-10-11

First stable release of the 2.22 line (the Rust and Qt rewrite). It contains
everything from the 2.22.0 betas; the changes since beta.32 are below.

### Added

- **Real hyperlinks**, link commands (open, edit, select, copy address, cut,
  copy, delete, remove) and the Hyperlinks List with NVDA add-on 1.1.0 (see
  beta.33).
- **Print and Print Preview draw the editor's own document**, so a printout
  is what the editor shows: fonts, styles, colours, tables and pictures
  (scaled to fit the page), page breaks, headers and footers, in colour. They
  used to be rebuilt in a hidden control from a simplified copy of the text.

### Changed

- **Credits checked against the originals.** The credits list was compared
  with each project's own license and README. Corrections: DTWAIN is
  Apache-2.0 (not LGPL); the Hunspell dictionaries now list each language's
  license and authors; the WordNet license is reproduced in full; FFmpeg's
  build source (BtbN) and GPL-3.0+ license, EPUBCheck's copyright holders
  (W3C, IDPF, Adobe), the Qt third-party notice and the Piper/Supertonic
  voice terms were added or corrected; DirectML was removed (not shipped).

- **About dialog: license, credits and disclaimer.** A "Show" list switches
  between About, License (built in, no longer read from a file that might
  be missing), Credits and third-party licenses (every library, tool,
  model and service ScanMaster uses, with its license; Qt's LGPL notice
  included) and Disclaimer (no warranty, check OCR/AI results,
  accessibility is not guaranteed, online services and your data,
  copyright, trademarks). LICENSE.txt and THIRD-PARTY-NOTICES.txt are also
  installed next to ScanMaster.exe.

## [Unreleased]

### Changed

- **Phase 1 dialog framework landed: F/R dialog migrated out of
  `main.rs` into a new `rust/scanmaster-app/src/dialogs/` module.**
  Tier 1 item 1 of `docs/plan-v2.22-phase1-dialogs.md`. Behavior
  preserved bit-for-bit (the `ScanMasterFindReplaceDialogClass`
  window-class name, the `FR_ID_*` child-control IDs, the
  `IDCANCEL == 2` close-button finding that makes `IsDialogMessageW`
  route Escape correctly, and the `Edit > Find` / `Edit > Replace`
  menu dispatch all unchanged). `main.rs` shrinks by 287 lines
  (3772 → 3485). Three new files: `dialogs/mod.rs`,
  `dialogs/framework.rs` (shared `control` factory, `LazyDialog`,
  `is_checked`/`get_control_text`/`set_control_text`/`set_checked`/
  `to_wide`/`module_handle` helpers, the `EDIT_STYLE`/
  `CHECKBOX_STYLE`/`PUSHBUTTON_STYLE` style-bit constants),
  `dialogs/find_replace.rs` (the migrated dialog), and
  `dialogs/find_replace_constants.rs` (constants split out so the
  example test can import them without dragging in the
  `crate::main`-dependent parts of `find_replace.rs`).
  `main.rs` exposes a new `pub(crate) fn richedit_bridge_clone()` so
  the dialogs module can reach the live `RichEditBridge`. New
  structural check `examples/find_replace_dialog_test.rs` asserts
  every constant the F/R dialog depends on (class name, title, 8
  child IDs, 3 style-bit masks, `to_wide` output) is identical to
  the pre-migration values. Tier 2-3 dialogs (Spelling, Speech
  Settings, Preferences, Font, Paragraph, …) will reuse this
  framework instead of repeating the `WNDCLASSW`/`thread_local!`/
  `IsDialogMessageW` boilerplate.

- **Phase 1 dialog scaffold landed: Spell Check dialog scaffolded
  on top of the dialog framework.** Tier 1 item 2 of
  `docs/plan-v2.22-phase1-dialogs.md`. The new
  `dialogs/spell_check.rs` + `dialogs/spell_check_constants.rs`
  declare the dialog's HWND slot and the
  `show_spell_check_dialog`/`route_spell_check_is_dialog_message`
  entry points `main.rs` needs, mirroring the shape of
  `dialogs::find_replace`. `main.rs` exposes three new
  `pub(crate)` accessors (`app_paths_for_dialogs`,
  `preferences_db_for_dialogs`, `speak_text_via_main`) so the
  dialog module can reach the live `AppPaths`, `PreferencesDb`,
  and `SAPI_VOICE` without taking internal dependencies on the
  thread-locals; the `app_paths`, `preferences_db`, `sapi5`, and
  `spell_checker` modules are now `pub(crate)` to support those
  accessors. The `Tools > Spelling…` menu item now opens the
  dialog (matches the C# `SpellCheckCommand → ShowSpellCheck()`
  binding; the previous `bridge_call!(...)` toggled the unrelated
  "live spell check" underline and was misrouted) and gains the
  `F7` accelerator matching the C# `InputGestureText`. The
  message-pump `IsDialogMessageW` routing now OR's
  `route_spell_check_is_dialog_message` alongside the existing
  F/R route. Full dialog body (15 child controls, `FindNext`
  loop, Change/ChangeAll/Ignore/IgnoreAll/Add/Undo, language
  combo, Pronounce/SpellOut/SpeakContext) lands in follow-up
  commits — this commit only ships the scaffold + plumbing so
  each follow-up diff stays reviewable. New structural check
  `examples/spell_check_dialog_test.rs` asserts every constant
  the dialog depends on (class name, title, 15 `SC_ID_*` child
  IDs in the 3201-3215 block, `IDCANCEL == 2` close button,
  `DEFAULT_SPELL_LANG == "en"`, `MAX_SUGGESTIONS == 32`) is
  identical to the values the C# `SpellCheckDialog.xaml`
  declares.

- **Phase 1 Spell Check dialog full body landed.** Direct port of
  `ScanMaster.App.Dialogs.SpellCheckDialog.xaml.cs`. All 15 child
  controls (`SC_ID_*` 3201-3215 plus `IDCANCEL == 2`) are created
  via `framework::control`; `WM_COMMAND` dispatch handles every
  button id. `FindNext` re-fetches the document and re-splits
  into words on every outer-pass iteration (NOT a stale pre-split
  list) so a ChangeAll auto-replace that changes text length never
  invalidates subsequent offsets — exactly the algorithm the C#
  version evolved to when its WPF TextPointer walks stopped
  reflecting live content. Session-scoped `ignored` HashSet
  (cleared on Close) and `change_all` HashMap (keyed by the
  cleaned alphabetic-only form) match Word's "Ignore" semantics
  and the C# `Stack<UndoEntry>` undo behaviour (only the top
  entry is ever consumed; ChangeAll rules are dropped on undo).
  Language combo enumerates `<home>/tools/dictionaries/*/`.aff,
  rebuilds the `SpellChecker` on selection, and persists via
  `prefs.spell_lang`. Pronounce / Spell Out / Speak Context go
  through `crate::speak_text_via_main(text)` so they share the
  live `SAPI_VOICE` the Speech > Read All menu already populates.
  New `dialogs/spell_check_logic.rs` hosts the pure (non-Win32)
  helpers `split_words` + `extract_paragraph_text`; the new
  `examples/spell_check_dialog_logic_test.rs` (14 assertions)
  exercises them without instantiating a real HWND — caught one
  bug mid-development (assumed `state-of-the-art` would be one
  word; the C# `[\p{L}']+` regex splits it into four). Together
  with the constants-only `examples/spell_check_dialog_test.rs`
  added in the scaffold commit, the dialog is now structurally
  pinned against drift in both UI layout AND core algorithm.

---

## [2.22.0-beta.34] - 2026-10-11

### Fixed

- **Preferences > AI Tasks: the model lists were empty for most
  providers.** They were only filled by "Refresh model lists", which
  needs the provider's API key and a network request and never ran on
  its own. Each list now starts with well-known models (and the model
  chosen for that provider on the AI page), and the page fetches the
  real list in the background for providers that have a key but no
  saved list.

## [2.22.0-beta.33] - 2026-10-11

### Added

- **Real hyperlinks.** Insert > Hyperlink (Ctrl+K) used to paste plain
  "text (address)". A link is now an address carried by the text: drawn
  blue and underlined, announced as "link" when the cursor moves onto it,
  and kept in .smdx, Word (as a real hyperlink), web pages and EPUB; links
  in Word documents and web pages are read as links.
- **Link commands.** With the cursor on a link, Ctrl+K edits it, and the
  context menu starts with Open Hyperlink (default browser), Edit
  Hyperlink (text and/or address), Select Hyperlink, Copy Hyperlink
  Address, Cut / Copy / Delete Hyperlink and Remove Hyperlink (keep the
  text).
- **Hyperlinks list** (Insert > Hyperlinks List, Ctrl+Shift+F7): every
  link with its address; go to, open, edit or remove. NVDA add-on 1.1.0
  maps NVDA+F7 to it, since the editor is not a browse-mode document and
  NVDA's own Elements List cannot list its links.

### Fixed

- **Crash on exit after a PDF had been opened** (0xC000000D) on machines
  without a GPU driver: Windows' PDF library tore down its software
  renderer after Windows had shut down the thread pool it needs. The
  process now ends just before that teardown (the test runner too).

## [2.22.0-beta.32] - 2026-10-10

### Added

- **Tables are a real grid for screen readers.** The editor now tells
  NVDA (through UI Automation) which table and cell the cursor is in:
  moving into a table says its size, moving between cells says the row,
  column and column header. Ctrl+Alt+arrow keys move by cell and say it
  ("Edge of table" at an edge), like NVDA's table commands in Word (NVDA
  only has those for Word and web pages, so ScanMaster provides them). Text in a table no longer reads Qt's hidden cell
  markers, and the stop just after a table reads as blank instead of the
  whole table.
- **Header rows.** Insert > Table has "First row is a header row"
  (ticked by default); header rows are the column headers screen readers
  say, and are kept in .smdx, Word (repeated header rows), web pages and
  EPUB (`<thead>`/`<th>`) and RTF, and read from Word and web pages.

### Fixed

- **Tab and Shift+Tab in a table move between cells** (the help said so,
  but Tab typed a tab character); each cell is said ("Age: 31, row 2,
  column 2"), and Tab in the last cell adds a row.

## [2.22.0-beta.31] - 2026-10-10

### Added

- **Earcons: hear formatting as you move.** Short sounds tell you what
  the cursor has reached: bold, italic, underline, strikethrough,
  superscript, subscript and highlighting starting and ending; each
  heading level; lists, tables and quotes starting and ending; links,
  pictures, text colour changes; comments and bookmarks. They play when
  you move the cursor (not while typing), and during Read All if you
  want. Preferences > Earcons turns them on or off, sets their volume,
  and chooses the earcon preset.
- **Earcon presets you can share.** Standard and Essentials are built
  in; make your own (changing a built-in one makes your copy), with any
  of 32 built-in sounds or your own WAV files for each event. Export saves
  a preset as one .smearcons file, sound files and all, to share; Import
  adds one.
- **Bookmarks stay on their text and are saved.** A bookmark is now on
  the character at the cursor, so it moves with the text, and it is saved
  in .smdx files (it used to be a position that drifted and was lost on
  closing). Inserting one plays its sound and says "Bookmark ... added"
  (no message box); Next / Previous Bookmark name each one ("2 of 4"),
  play the bookmark sound and wrap round; reaching a bookmark gives a bell
  and its name, a line with one a soft tick. Manage Bookmarks lists them
  in text order with their text; Enter goes to one, Escape closes.

- **You can hear comments.** When the cursor moves onto commented text
  you hear a short chime and the comment is read out ("Comment by Sam:
  check this date"); moving to a line with a comment on it gives a softer
  note; during Read All you hear just the sounds. Inserting a comment
  plays the chime and says "Comment added" (no more message box to
  dismiss). Preferences > Speech > Comment feedback picks sound and
  speech, sound only, speech only or off. The speaker-style and equation
  announcements also now work for plain arrow-key moves, not just
  selections.

- **Comments and bookmarks in Word, web pages, EPUB, RTF, Markdown and
  PDF.** Word (.docx): real Word comments (author, date, resolved) and
  bookmarks, both ways - ones made in Word come in too (checked in Word
  itself). Web pages and EPUB: a numbered link after each commented
  passage, the comments listed at the end (an EPUB page of their own) with
  links back, bookmarks as link targets; reopening brings them back
  (EPUBCheck: no errors). RTF: comments with author and date, and
  bookmarks, as Word reads them. Markdown: comments as footnotes,
  bookmarks as link targets. PDF: numbered comments listed at the end,
  bookmarks in the PDF's outline.

### Changed

- **Comments stay on their text and are saved.** A comment is now kept
  on the words it is about (the selection, or the word at the cursor), so
  it moves with them as you edit; it used to be a fixed position that
  drifted, and comments were lost when the document was closed. They are
  saved in .smdx files, and saved web pages show each comment on its
  text. Next / Previous Comment go in text order, say "2 of 5" and wrap
  round.
- **Manage Comments works from the keyboard.** Tab now reaches every
  button (the comment text box used to keep it), the buttons are always
  available, the first comment is selected when it opens, Enter or a
  double-click goes to the comment, and Escape closes. New Add button;
  Resolve becomes Reopen on a resolved comment; Delete also takes the
  comment off its text. The list is in text order and shows the text each
  comment is on.
- **Check Heading Structure: Enter goes, Escape closes.** The first
  problem is selected; Enter (or a double-click) closes the list and puts
  the cursor on that heading; Escape closes without moving the cursor.

### Fixed

- **RTF export put a stray space before plain text** (every run without
  formatting started with one, so "Two paragraphs" came out with double
  spaces).
- **EPUB export of a document without a title or author was invalid**
  (empty title and creator); it now uses "Untitled" and leaves the
  creator out.
- **Text with "&", "<" or ">" lost those characters when a .smdx
  document was reopened** ("Fish & Chips" came back as "Fish  Chips"),
  as did characters written as references. The reader now keeps them.

## [2.22.0-beta.30] - 2026-10-10

### Changed

- **Help opens in your web browser**, as the real web pages it is:
  headings to move by (H with NVDA or JAWS), links to follow, real lists
  and tables, and the browser's find (Ctrl+F). F1 opens the manual, Help >
  Quick Start and Help > Keyboard Shortcuts their own pages. The help used
  to be a window of its own showing each page as plain text, with no
  headings or links to move by, all on one line, and with the page's
  style sheet read out at its start.
- **The help has a full table of contents and a new design.** A Contents
  page lists every topic and every section in it, as links; each topic
  starts with "On this page" links to its sections, and has a header with
  Contents and the previous and next topic, a "Skip to main content" link,
  and a footer with previous / next, Contents and Back to top. One shared
  style sheet gives every page the same clean look, in light or dark
  following Windows, in Windows high contrast, in narrow windows and in
  print. The contents, section links, header and footer are generated by
  scripts/build-help.py (run by the release build), and a test checks
  every link, every section anchor and each page's heading structure.
- **Display settings in the help, for different needs.** A Display
  settings button on every help page opens a panel with ready-made
  settings for low vision (150% text, high contrast, large-print font,
  wider spacing, underlined links), dyslexia (cream background,
  dyslexia-friendly font, wider spacing) and light sensitivity (dark), or
  each part separately: colours (automatic, light, dark, two high-contrast
  schemes, cream), text size (100-200%), font (standard, large print,
  dyslexia-friendly, serif), wider line/letter/word spacing and always
  underlined links. The choices are kept for every page and applied
  before a page is drawn; Reset goes back to standard.

### Fixed

- **Text straight inside a container was dropped when opening HTML or
  EPUB** - a tip box's text, a definition, a page footer. It is kept now.
- **The menu arrow (›) and other signs vanished** when opening HTML,
  EPUB or Markdown: they are known now (‹ › arrows, spaces, minus,
  ≤ ≥ ≠ ≈ ∞ ✓).

## [2.22.0-beta.29] - 2026-10-09

### Added

- **Talking books from Save as Audio: DAISY 2.02, DAISY 3 (ANSI/NISO
  Z39.86-2005) and EPUB 3 with media overlays.** The text and its audio
  together, read with the chosen speech profile (voice, rate, pauses,
  styles, effects); each paragraph is timed exactly, so players highlight
  it as it is spoken and move by heading. Also in Batch Convert.
- **A voice for picture descriptions.** A new speech element, Image
  Description (Speech Settings > Document Elements), reads every picture
  description in its own voice, rate, pauses and effects: a picture's alt
  text ("Image: ..."), long descriptions added by Describe Image and
  Describe All Images, and PDF import's page descriptions - when reading
  aloud, in Save as Audio and in talking books. Descriptions ScanMaster adds
  are marked with the new Image Description character style; Format >
  Character Style > Image Description (Ctrl+Alt+Shift+5) marks others.
- **Talking books are checked.** Every book is checked when it is made
  (each link, id and file, each paragraph's place in the audio, and the
  heading outline), and an EPUB also with EPUBCheck, W3C's official EPUB
  checker, now included (installer component "EPUBCheck", on the bundled
  Java). The result is shown when the book is done; problems are listed.
  Books made by Save as Audio were also checked during development with the
  official DAISY validators (DAISY Pipeline 2's DAISY 2.02 and DTBook
  validators, and every DAISY 3 file against its ANSI/NISO Z39.86-2005
  DTD) and EPUBCheck: no problems (`scripts\validate-talking-books`).
- **Heading structure is checked before a talking book is made**: a first
  heading below level 1, a skipped level, an empty heading, a heading so
  long it is probably a paragraph, or no headings are named, with the
  choice to make the book anyway (its levels corrected) or fix them first.
  An EPUB whose text starts before the first heading now starts with the
  book's title as its level 1 heading, so its outline starts at level 1.
- **Heading level is a spin box** in Save as Audio, stepping through the
  heading levels the document actually has.
- **Separate files go in a folder named after the document** (inside the
  folder chosen), with an option to zip the folder too. A folder already
  holding an earlier export gets a new name ("Book (2)") instead of being
  mixed with it.

### Fixed

- **Picture descriptions were not read aloud.** Read All and Read From
  Cursor skipped a picture's description (its alt text); they now read it
  ("Image: ..."). PDF import's "Describe images" stored its descriptions
  where nothing showed or read them; they now appear after the page's
  text ("Image description: ...") and are read, in audio files too.
- **An EPUB's identifier is a real UUID** (EPUBCheck warned about it).
- **Save as Audio suggests the document's own file name** with the
  format's extension (it used to start with an empty name).

## [2.22.0-beta.28] - 2026-10-08

### Added

- **Equations in tagged PDFs are formulas.** Saved as PDF, each equation
  is tagged as a Formula whose alternative text is how MathCAT speaks it
  ("x is equal to the fraction with numerator ..."), as PDF/UA requires,
  so screen readers read it properly; it used to be ordinary text.

## [2.22.0-beta.27] - 2026-10-07

### Added

- **Equations are kept as mathematics and read by MathCAT.** Each
  equation is stored as MathML, shown in the editor as one readable line
  (`x = (−b ± √(b² − 4ac))/(2a)`), and spoken by MathCAT (DAISY's math
  speech engine, the one behind NVDA's MathCAT add-on, now built in):
  "x is equal to the fraction with numerator negative b plus or minus the
  square root of …". Word equations (Office Math: fractions, scripts,
  roots, sums and integrals, brackets, functions, limits, accents, bars,
  boxes, equation arrays, matrices) and MathML in web pages and EPUB books
  are brought in whole - Word equations used to be flattened to their
  characters ("A=πr2"). Read All, Read From Cursor and Save as Audio
  speak equations as MathCAT does, in the voice of the paragraph or
  speaker they're in; the screen reader is told an equation when the
  cursor moves onto it. Kept in .smdx, HTML and EPUB (as MathML, with
  the EPUB `mathml` property), Word (as Word equations) and Markdown (as
  LaTeX).
- **Insert › Equation (Alt+=) takes LaTeX** and makes a real equation;
  "Spoken as" says how MathCAT will read it while you type. On an
  equation it edits it (also Edit Equation on the context menu). It used
  to type the LaTeX in as plain text.
- **Explore Equation (Alt+Shift+=)**: arrow through an equation part by
  part with MathCAT's navigation, as in NVDA's MathCAT add-on, with the
  braille (Nemeth or UEB) on the status bar; Escape stops.
- **Equations from OCR**: Mathpix and Mistral OCR results (and LaTeX in
  Markdown: `$...$`, `$$...$$`, `\(...\)`, `\[...\]`) become equations.
- **Preferences › Speech › Mathematics**: speech style (ClearSpeak,
  SimpleSpeak, MathSpeak), detail, and braille code.

### Fixed

- **Character styles were lost, but for their first character, when a
  document was opened again.** Qt gives an anchor's name to its first
  character only, so a speaker's words came back with just the opening
  quote mark in that speaker's style. The editor is now told how long
  each styled stretch is.

## [2.22.0-beta.26] - 2026-10-07

### Fixed

- **SAPI tags were read out instead of obeyed.** Reading renders the
  speech ahead, and the SAPI voice was always given the text as plain
  text, so a tag such as `<rate speed="5">` was spoken aloud. SAPI voices
  now get each piece as SAPI XML - tags still open from an earlier piece
  re-opened, other `&` and `<` escaped, the voice's word positions mapped
  back so the cursor still follows - and other engines get the text
  without the tags, with `<silence>` as a pause. The same in Save as
  Audio (where a tag only worked if the paragraph began with it).

### Added

- **Character (inline) styles, for speakers in a dialogue.** Format >
  Character Style (also on the context menu) puts Speaker 1-4
  (Ctrl+Alt+Shift+1-4) on the selected words, or your own character
  styles made in the Styles dialog (new Type: Paragraph / Character, with
  optional bold, italic, underline, colour and font); Remove Character
  Style (Ctrl+Alt+Shift+0) takes it off. Speech Settings > Document
  Elements lists them, so each speaker gets a voice, rate, pauses and
  effects: reading aloud and Save as Audio switch voices inside the
  paragraph. The screen reader is told the style's name when the cursor
  moves into it. Kept in .smdx, Word and HTML files.
- **Delete on the Edit and context menus.** Edit has Delete (the
  selection, or the character after the cursor), Delete Previous
  Character, Delete Word and Delete Previous Word, shown with their keys
  (Del, Backspace, Ctrl+Del, Ctrl+Backspace); the editor's context menu
  has Delete. They do exactly what the keys do (the editor is handed the
  same key press, so undo and screen-reader output match), and each can
  have an extra shortcut in the Keyboard Manager while the keys
  themselves keep working as before.

---

## [2.22.0-beta.25] - 2026-10-06

### Fixed

- **Voice Effects returned to the editor.** Pressing OK in Voice Effects
  (and closing the delete confirmations and pronunciation boxes) put
  focus back in the editor with Speech Settings left behind it, so the
  effect couldn't be tested or saved. These windows now belong to Speech
  Settings, and Voice Effects returns to its button. The same fix for
  Keyboard Manager's New Profile box.

---

## [2.22.0-beta.24] - 2026-10-06

### Fixed

- **Voice effects are heard when reading aloud.** A profile with a
  Document Elements style that has its own voice (for example Heading 1
  in another voice) was read straight through the SAPI voice, with no
  effects at all and for SAPI 5 only. Every reading now goes through the
  rendered pipeline: styles get their own voice, rate, pauses and
  effects with every engine, and the profile's effects apply everywhere
  else. Switching voices between styles no longer re-prepares the voice
  each time.
- **Test Voice plays the chosen effects**, before they are saved (it
  used to speak straight through the voice).
- **Effects chosen with no speech profile were thrown away**; a profile
  named Default is now made for them.

---

## [2.22.0-beta.23] - 2026-10-06

### Added

- **Preferences > AI Tasks: a provider and model for each AI job** -
  OCR (Upload to AI, including the document services), proofreading,
  layout, image descriptions, grammar checking, the AI Assistant and the
  Dictionary - so each can use the model that suits it. "Default" uses
  the AI page's provider and its model; Refresh model lists fetches the
  lists for the providers in use; a warning shows when a job that sends
  pictures is given a provider that can't read them.
- **Grammar checking with AI.** LanguageTool stays the default; with an
  AI model chosen for Grammar checking, Tools > Grammar checks the
  selection (or the whole document) with it, and its findings go in the
  same list with Apply and Apply All. Its prompt is editable on the AI
  page.

### Fixed

- **Each AI provider remembers its own model.** The model was one
  setting for every provider, so after a restart each showed the last
  model picked anywhere.
- **After an update, ScanMaster comes back in front.** Restarted by the
  updater (also after a failed update) it opened behind other windows,
  went unnoticed, and then blocked the next update and the installer.

---

## [2.22.0-beta.22] - 2026-10-06

### Fixed

- **Updating a portable copy failed when a second ScanMaster window was
  open.** The update helper waited only for the window that started the
  update; another window (or the launcher each window keeps running)
  still held `ScanMaster.exe`, so the update stopped with "the process
  cannot access the file", rolled back and left the old version. It now
  waits for every ScanMaster program running from the folder, and after
  20 seconds names what is still open and asks to close it (Retry) or
  keep the current version (Cancel).
- **Updates now use the new version's update helper** (taken from the
  downloaded zip), so a fix to the updater applies to the update that
  delivers it instead of needing a manual update.

---

## [2.22.0-beta.21] - 2026-10-06

### Fixed

- **A portable copy's API keys (and other settings) now go with it to
  other computers.** Every setting was encrypted with Windows DPAPI,
  which only the same Windows user on the same computer can read, so on
  another computer the keys read back as blank - and saving Preferences
  there wrote the blanks over the real keys, so they were gone on the
  first computer too. A portable copy now encrypts its settings with a
  key kept in its own database (settings this computer can still read
  are converted the first time it starts), and a value that can't be
  read is never overwritten by a blank. Installed copies keep DPAPI.

---

## [2.22.0-beta.20] - 2026-10-06

### Fixed

- **Save as Audio / Batch Convert: no more pauses in the middle of a
  sentence.** Text and PDF books hold one paragraph per printed line;
  each line was voiced on its own with a 0.3 s gap, so every line break
  was a pause and a fresh start of the intonation. Lines that run on are
  now joined back into sentences (a word hyphenated at the line end is
  rejoined). Kokoro also left about 0.8 s of its own silence at every
  join, and cut any paragraph over 510 phonemes short; it now speaks a
  sentence at a time with its silence trimmed (live reading too).
- **Choosing a speech profile applies all of it.** The dialog opens with
  the active profile applied (it used to show it selected with the
  engine and voice still at their defaults); a profile ticks "Use the
  profile's style settings" when it has any, and those per-style voices,
  rates, volumes, pauses and effects now work with every engine, not
  only SAPI 5. The profile's volume now applies to every engine, and the
  Preferences sentence and paragraph pauses are used in audio files.
- **NVDA no longer waits a few seconds after a book opens.** Qt decoded
  every image on the UI thread during the layout after loading, only to
  learn its size, in slices of up to 0.35 s that each screen-reader
  request had to wait out. Images now get their size from the file
  header: on Pro Git the busy time after opening fell from about 1.1 s
  (until 1.85 s) to 0.2 s (until 0.6 s).

---

## [2.22.0-beta.19] - 2026-10-05

### Fixed

- **Check for updates closed ScanMaster without installing the update** (from beta.16 on). The update
  helper inherited ScanMaster's output, which closes with ScanMaster, and stopped at its first progress
  message before changing anything. It now writes its progress to its log only, reports any failure in a
  message, and is started without ScanMaster's output. **Copies on beta.16, beta.17 or beta.18 need one
  manual update** (run the new Setup, or unzip the new portable ZIP over the old folder); after that,
  updates install by themselves again.
- **Upload to AI: "the book could not be loaded because the editor was closed".** With "Also open the
  structured JSON", the converted book and its JSON opened at the same moment; for a long book both load
  in the background, and the second load cut the first one off, which then closed the book's tab. New
  tabs now open one after the other, and a background load follows its own tab even when another tab
  is active.

---

## [2.22.0-beta.18] - 2026-10-05

### Fixed

- **Reading with online voices (such as Andrew) no longer stops for a break every so often.** When
  Microsoft's voice service was slow to answer a sentence, the reading switched to a slower way of
  speaking with a pause of several seconds; it now asks again and carries on.
- **Save as Audio:**
  - Much faster with online voices: the book is made a few paragraphs at a time, several at once.
    A five-page sample took 18 seconds instead of over two minutes.
  - The progress window counts parts as they finish; it used to stand still until the whole book was
    done, which looked like a freeze.
  - With one file per heading or per page count, each file is written as soon as its chapter is done;
    before, nothing was written until the end. Cancel stops within a few seconds and keeps the files
    already made.
  - Audio files and audiobooks carry the book's title and author (from Document Properties, or the file
    name); they had none.
  - Batch Convert to Audio's status line shows which book and part is being made; it never changed.
  - Choosing the output folder uses the standard Windows folder picker, with a Folder box to type a path.
  - Tested: single file, single file with chapter markers (M4B and MP3), separate files by heading and by
    page count, batch conversion, and every format (MP3, M4A, M4B, FLAC, WAV, OGG).
- **No more console windows popping up** while exporting audio, reading scans with Tesseract,
  converting with Pandoc, checking grammar or finding network scanners.
- **Print Preview no longer freezes ScanMaster for up to a minute** with printers that are slow to
  answer the first time (seen with a network printer): the default printer is contacted in the
  background when ScanMaster starts, and Print Preview says "Contacting the printer…" if it isn't ready.
- **OpenAI's newer models** refused requests ("'max_tokens' is not supported with this model. Use
  'max_completion_tokens'"); ScanMaster now sends what OpenAI expects, and leaves out the temperature
  for models that accept only the default.

### Changed

- The log (`scanmaster.log`) records reading and audio export: the engine and voice, each file written,
  any wait for the voice and any error, to help with problem reports.

---

## [2.22.0-beta.17] - 2026-10-05

### New

- **Headers and footers for all pages, odd and even pages, the first page, or a single page**
  (Insert > Header and Footer):
  - "Different even and odd pages" and "Different first page" give those pages their own header and
    footer; "This page only" gives the page you're on its own, or none.
  - The header and footer boxes keep formatting: bold, italic and underline (Ctrl+B, Ctrl+I, Ctrl+U), left,
    centre or right alignment (Ctrl+L, Ctrl+E, Ctrl+R or the Align list), and font, size and colour
    (Font…).
  - Fields for the page number, page count, date and title ({PAGE}, {PAGES}, {DATE}, {TITLE}) are filled in
    when printing, for example "Page 3 of 10".
  - The distance of the header and footer from the paper's edge can be set.
  - **Printed exactly as formatted**, and shown in Print Preview. Saved PDFs carry them too, as page
    furniture that screen readers skip.

### Fixed

- **Printing and Print Preview used only about a third of the page**: page sizes and margins were handed
  to Windows in the wrong unit. Pages now print at their real size, with the margins from Page Setup.
- **Red and blue were swapped** in printed text colours (and in the older RichEdit editor).
- Reloading formatted text into a rich-edit box no longer carries over the previous text's bold, italic,
  font or colour.

---

## [2.22.0-beta.16] - 2026-10-05

### New

- **Account and limits** on the Cloud OCR and AI pages of Preferences, for each provider:
  - **Check account** shows what the provider tells an API key: for OpenRouter, credits bought, used and
    left, the key's own spending cap and what's left of it, and free-model requests left today; for Mathpix,
    this month's usage; for HuggingFace, the plan. The others don't report a balance, so the check confirms
    the key works.
  - **Test connection** sends one small real request (a one-word question to the model, or a small test
    picture to the OCR service) and shows how long the answer took and what came back, including the
    provider's own error.
  - **Buy credits** and **Price list** open the provider's billing and price pages in your browser.
  - **Prices:** the price of the model chosen on the AI page, per million tokens in and out, looked up live
    (for OpenAI, Anthropic, Google and Mistral models through OpenRouter's public list, which charges their
    own prices); the OCR services' page prices.
  - **Limit per minute and Speed:** the provider's pages or requests per minute (filled in by itself when
    the provider reports it, for example Mistral's 125 OCR pages a minute) and a slider from 10% to 100% of
    it. Imports and AI requests keep under the chosen share.
- **Debug output window** (Preferences > Advanced > Show the debug output window): Scan Master no longer
  opens a terminal window when it starts. Its diagnostic output goes to a window you show or hide with this
  check box; closing that window just hides it.

### Fixed

- **Insert > Table** made a real table; it used to type "[Table: 3 rows x 4 cols]". Inserting any piece
  that starts with a table (Insert > File too) no longer loses the table's first cell.
- **Insert > Footnote and Endnote** ask for the note's text, put its number at the cursor, and add the
  note under a Footnotes or Endnotes heading at the end, numbering on from the notes already there. They
  used to insert a bare "1".
- **F6** now also reaches the Formatting toolbar and the page viewer (View > Image Only, Both), and
  **Tab** moves between the page viewer's buttons.
- **AI prompt box** (Preferences > AI): Tab moves on to the next control instead of being trapped; Enter
  still starts a new line.
- **User manual** brought up to date throughout: screen layout and F6 order, settings location, Speech
  menu commands (reading piece by piece, rate, volume and pitch, SAPI tags), Preferences pages (Spelling,
  Grammar, OCR, Speech, Keyboard, Advanced), footnotes, tables, headers and footers, clips, accessibility
  templates, Scanner Diagnostics, system requirements, and the removal of things that were only in the
  older version.

---

## [2.22.0-beta.15] - 2026-10-04

### New

- **Page clean-up for scans and camera pictures** (Tools > Preferences > Scanning > Page clean-up): split
  facing pages, correct page orientation (sideways and upside-down pages), deskew, straighten text lines,
  correct image resolution (to 300 dpi), detect page edges, whiten background, reduce ISO noise, remove
  motion blur, correct trapezoid distortions, fix inverted colors, convert to black and white, and remove
  color marks. Each scanned page is cleaned up before OCR reads it; a split book spread becomes two pages.
- **Page viewer:** View > Image Only and Both now have a bar with First page, Previous page, Next page,
  Last page and Go to page, and say which page you're on. Image Only uses the whole window, and pages
  are shown at their real proportions.
- **Two pages side by side** (View > Two Pages Side by Side, or "Two pages" on the bar), like an open book.

### Fixed

- **Text cut off in dialogs** ("Operatio" for "Operation" and dozens more, in Preferences and other
  dialogs): dialogs now use the standard Windows font, and any label that still doesn't fit is widened.
- **Update dialog:** OK is the default button (Enter chooses it) and the dialog is shorter. (Updating from
  beta.11 or older: OK is below the window's edge there; press Tab once, then Enter.)

---

## [2.22.0-beta.14] - 2026-10-04

### New

- **Accessible PDF.** Saving or exporting as PDF now makes a tagged PDF that follows PDF/UA-1, the
  standard for accessible PDF: headings (also as bookmarks), paragraphs, lists, tables with header cells,
  pictures with their alt text, the document language and every paragraph in another language, and the
  title, authors, subject and keywords. Page numbers are marked so screen readers skip them. A picture
  without alt text is called "Image without a description", and you're told how many there were.
- **Insert > File** puts another document in at the cursor, with its headings, lists, tables, pictures and
  language marks, to combine several files into one. One Undo removes it.
- **Format > Detect Languages with AI** finds the document's main language and every paragraph written in
  another one, and marks them, so screen readers switch voice and spelling uses the right dictionary.
- **Language marks are saved in EPUB, Word and RTF** (and read back from Word, RTF and HTML), as well as
  HTML, ScanMaster files and PDF.
- **Describe images by type of graphic.** Describe Image with AI uses a prompt made for the kind of picture
  — bar chart, map, equation, flow chart, photograph and 130 more — detected automatically or chosen, as
  short alt text or a long description (with tables and lists) added after the image.
- **Format > Describe All Images with AI** describes every picture in any document, not only scans.
- **The editor's context menu** (right-click, Applications key or Shift+F10) now has Describe Image,
  Describe All Images, Dictionary, Thesaurus, AutoCorrect and Styles as well as the editing commands.
  Right-clicking a picture puts the cursor on it.
- **File > Document Properties**: title, authors, subject, keywords, publisher, ISBN, publication date and
  language, with "Fill with AI" reading them from the start of the document. Saved in EPUB, Word and
  ScanMaster files.
- **Upload to AI** can keep the figures of a PDF as real pictures ("Markdown, keeping figures") and
  describe every figure by type. PDF import describes images by type too.

### Fixed

- **NVDA says "graphic"** (and the alt text) for pictures in the editor, instead of "question mark".
- **Speech rate and volume** now change speech while a document is being read, Preferences applies them at
  once, and Speech Settings no longer puts old values back.
- **The default sound card** is used when the chosen one is unplugged or turned off.
- **Format > Language** did nothing in the editor; it works now.
- **Kokoro voices:** no more false "voice is not available" message, and reading starts at once after the
  first time (the voice stays loaded; choosing it in Speech Settings starts loading it).
- **Plugin Manager:** the button says Uninstall for an installed add-on and Install otherwise.
- ScanMaster no longer crashes as it closes after a PDF has been imported.

---

## [2.22.0-beta.13] - 2026-09-27

### New

- **File > Upload to AI.** Send a file to an AI provider and get it back as a structured document you can
  read and edit: real headings, lists, tables, quotes and image descriptions, opened as a new untitled tab.
  - Works with every AI provider (OpenAI, Anthropic Claude, Google Gemini, Mistral AI, OpenRouter, Ollama,
    Ollama Cloud, HuggingFace) and with the document services from PDF import (Mistral OCR, Mathpix,
    Datalab, Docling).
  - Choose the file (Browse…), the provider and the model; the prompt is saved for next time.
  - PDFs, pictures and any document ScanMaster opens can be uploaded. PDFs go to Claude, OpenAI, Gemini and
    OpenRouter as documents and to the others as page pictures; long files are sent in parts, and parts
    already converted are kept if a later one fails.
  - "Also open the structured JSON" opens the JSON the document was built from in a second tab.
  - Uploads run in the background with a progress window; Cancel stops at once.
- **Each provider's models are listed as soon as you choose it** (the last list shows at once, then the
  current one loads); models that can't read files (embeddings, speech, image generation) are left out.

### Fixed

- **Local Ollama:** requests now ask for a context window big enough for the text, images and reply
  (Ollama's small default rejected page images), and local models get up to 30 minutes per request instead
  of 2. This also helps the AI Assistant and Describe Image with Ollama.

---

## [2.22.0-beta.12] - 2026-09-27

### New

- **Effect presets you can name and edit.** Tools > Preferences > Effect Presets: choose an effect (Reverb,
  Echo, Compression, Chorus, Distortion, Flanger, Gargle, Equalizer), see its presets, and create, edit,
  rename or delete them, with every setting of the effect. In Speech Settings, Voice Effects and Element
  Effects now simply pick Off or a preset for each effect; editing a preset updates every voice that uses it.
- **Every command can have a shortcut.** The Keyboard Manager now lists every menu command (Thesaurus, the
  absolute rate/volume/pitch settings and all SAPI tag commands were missing), and the shortcut shown in
  each menu is always the one that really works, updating as soon as you change it.
- **New default shortcuts** that the menus used to show but never worked: speech navigation (word
  Ctrl+Alt+Left/Right, line Alt+Up/Down, sentence Alt+Shift+Left/Right, paragraph Alt+Shift+Up/Down),
  rate Ctrl+[ / Ctrl+], volume Ctrl+Shift+[ / Ctrl+Shift+], Insert Date and Time Alt+Shift+D, Scan
  Ctrl+Shift+Q, Camera Ctrl+Shift+C, Insert Comment Ctrl+Alt+M, find quoted text Alt+Q / Alt+Shift+Q.
  Zoom In is now Ctrl+numeric-keypad-plus (Ctrl+= is Subscript).
- **Add Autocorrect Entry for Word (Ctrl+Space)** now works: it opens Autocorrect with the word at the
  cursor (or the selection) ready for its replacement.

### Fixed

- **Focus lands where it should.** After a message box or another window closes (for example "Loaded N
  models" after Refresh models), focus goes back to the control you were on instead of the dialog itself.
  When a task finishes, focus moves to its result and the outcome is spoken (AI answers, image
  descriptions, grammar issues, device and language lists, add-on installs, conversions, scans).
- **Dialogs are fully visible:** they open centred over ScanMaster and are sized to show all their controls
  (Preferences' OK and Cancel, the small prompts and Word Count were cut off). Missing labels added and
  duplicate Alt letters removed across many dialogs.
- **Spelling (F7)** used the Czech dictionary for English (so ordinary words were flagged and it took
  half a minute to open). It now uses US English, opens at once, starts at the cursor, highlights the right
  word, skips words in capitals and says when the check is complete.
- **Reading has no extra pauses** between pieces of text; only the sentence and paragraph pauses set in
  Preferences are used.
- **Scanning (WIA)** failed with "No scan item found"; the scanner's page source is now found.
- **Adding a shortcut:** Alt combinations can be captured, keys already in use are moved only after asking,
  and keys that typing needs are refused. Shortcuts work reliably while the editor has focus.
- AI Assistant, Describe Image and the Dictionary's AI synonyms no longer freeze ScanMaster while waiting.
- Help > Release Notes shows the release notes (it always said they couldn't be found).

---

## [2.22.0-beta.11] - 2026-09-26

### New

- **Choose where speech plays:** an **Output device** list (System default, or any speakers, headphones,
  USB or virtual audio device) in Tools > Preferences > Speech and in Speech > Speech Settings. Both show
  the same choice, it is saved in your speech profile, and every voice uses it, SAPI 5 included.

### Fixed

- **Read All and Read from Cursor start straight away on big books.** On a large EPUB, reading could stay
  silent for 7-10 seconds (so it looked as if it didn't work): ScanMaster was busy for several seconds
  after opening the book, and the whole book was handed to the voice in one piece. Reading now starts in
  about a second.
- **Chunk granularity is honoured by SAPI 5 voices too** (sentence, line, paragraph, page, section, ...),
  and Preferences and Speech Settings no longer overwrite each other's choice. Preferences also offers
  Section.
- Voice styles for document elements no longer slow down the start of reading.
- Saving a profile in Speech Settings no longer resets its output device and pan.

---

## [2.22.0-beta.10] - 2026-09-26

### Important

- **The updater now actually updates.** Before, ScanMaster downloaded an update, said "please restart"
  and stayed open, so nothing could be replaced (portable copies rolled back after 10 seconds; the
  installer found ScanMaster's files in use). Now ScanMaster closes itself after the download (asking
  you to save first), the update is installed, and ScanMaster starts again by itself. **If you are on
  beta.9 or earlier, install this version by hand once** (download the setup or the zip); later updates
  work automatically. The update dialog now shows full versions (for example v2.22.0-beta.9 to
  v2.22.0-beta.10).

### New

- **Scanning:** Scan + OCR really recognises the text now (it used to insert only the picture), with
  Windows OCR, Tesseract, PaddleOCR or the Mistral, Mathpix and Datalab cloud engines. Each scanned page
  becomes its own page before or after the current one, at the beginning or at the end, and keeps its
  picture (View > Image Only or Both). Manual mode offers **Scan Next Page**. The resolution list comes
  from your scanner. "Scan in background" and the default operation, OCR engine and language from
  Preferences are used.
- **OCR Current Page** (Ctrl+Shift+O) and **OCR All Pages** re-read pages from their scanned pictures;
  Recognize Pages and the Scan dialog's OCR Only do the same.
- **Kindle books without DRM open:** .mobi, .azw3, .azw and .prc, with title, author, pages and
  pictures. Protected books and .kfx files get an explanation instead.
- **Old Scan Master documents (.smf)** open.
- **Pictures in Word documents** come in, including Mathpix's Word output.
- **File > Export As** saves a copy in another format without changing the open file.
- **View > Read Status Bar** speaks the status line.
- **Preferences that now work:** theme (light, dark or follow Windows: editor, title bar, menus,
  toolbars and side panes), toolbar style (icons, text or both, with a full Standard toolbar), back up
  on save (keeps name.ext.bak), lines per scroll, show status bar / page image sidebar, document
  language and right-to-left direction, and an editor for the three AI prompts.
- **Speech:** reading highlights (word, sentence, paragraph), read on caret move, chunk size for neural
  voices, and neural voices follow your volume and voice effects. Rate and volume from Speech Settings
  are remembered.
- **Qt editor:** autocorrect and sentence capitals, live spelling marks, Tools > Language, Shift+Tab
  outdent, and the Bold/Italic/Underline buttons follow the selection.
- **Scanner Diagnostics** lists each camera's video modes.

### Fixed

- **Positions in the editor no longer drift after each paragraph:** go to line, find and replace, sort
  lines, page commands, autocorrect and spelling marks were off by one character per paragraph.
- **Saved View settings** (toolbars, panes, zoom, browse mode) are restored at startup again.
- **PDF export:** every page starts a new PDF page, and files are about 9 times smaller.
- **Docling import:** headings get levels from their printed size instead of all being Heading 2.
- **HTML import** no longer loses content after a stray closing tag.
- Long text in dialog boxes is no longer cut off at 512 characters.
- Scan Master closes properly when Windows shuts down or an installer asks it to.

---

## [2.22.0-beta.9] - 2026-09-26

### Fixed

- **Cancel works during cloud OCR and Docling imports.** Cancel is always available and takes you
  straight back to the editor, even while a request is still in progress or ScanMaster is waiting
  out a rate limit (anything that comes back later is ignored). Before, a failing Mistral import
  could not be cancelled and ScanMaster looked frozen for minutes.
- **The import progress window says what it is waiting for**, for example "The OCR service is
  limiting requests (HTTP 429). Trying again in 60 seconds (attempt 2 of 6)".
- **Import error messages no longer get lost:** they are attached to the main window instead of
  the progress window that had just been hidden.
- **Speech says when it can't use your choice:** if the configured speech engine isn't installed in
  this copy, or the saved voice isn't on this computer, Read All and Read from Cursor now say so
  instead of silently reading with SAPI's default voice.

---

## [2.22.0-beta.8] - 2026-09-26

### New

- **New text editor (Qt).** The editing area is now built on Qt instead of the Windows RichEdit
  control, with its own accessibility support tuned for NVDA: reading by line, word and character,
  blank lines, and the status bar. Large documents load in the background with a percentage shown,
  so the window stays usable.
- **Docling: offline PDF import that keeps the structure.** Install "Docling document layout" from
  Tools > Plugin Manager (285 MB). The PDF Import dialog then offers "Docling (local, keeps headings
  and tables)", and Auto uses it too. Text PDFs and scans come in with headings, bulleted and
  numbered lists, real tables, code examples and pictures with captions, in reading order, with
  running page headers and page numbers removed. Nothing is sent over the internet. Scans are read
  with Tesseract, so all installed Tesseract languages work.
- **PowerPoint and Excel files open** (with the Docling add-on): each slide or worksheet becomes a
  page, with slide titles and sheet names as headings.
- **Cloud OCR engines in PDF Import:** Mistral OCR, Mathpix and Datalab. The whole PDF is sent
  in one request (large books in parts) and comes back as a structured document; Mathpix returns
  a Word document. Mistral's model can be chosen, with a Refresh button that lists the models
  your account can use.
- **Save as a web page with images:** choose "Web Page with Images (*.zip)" in Save As to get
  `index.html` plus an `images` folder. Opening that ZIP brings the pictures back. Plain `.html`
  saves now keep their pictures inside the file.

### Fixed

- **Browse mode** (View > Browse Mode, Ctrl+Shift+`) works with the new editor: H, T, L, Q, G and
  1-6 move to the next heading, table, list, quote, picture or heading level (Shift goes back) and
  are announced, instead of typing the letter into the document. T, L and G now move to the next
  table, list or picture rather than the next page containing one.
- **Saving keeps formatting:** bold, italic, underline, strikethrough, super/subscript, lists,
  tables, alignment and named styles are now saved from the editor; before, a save kept only the
  text and heading levels.
- **Named styles** (Caption, Quote, your own styles) are kept when a document is reopened.
- **Heading sizes:** the built-in heading styles were ten times too large when applied, in the
  Styles dialog, and in Word/HTML exports (Heading 1 came out at 240 pt). Documents saved with the
  old sizes are corrected when opened.
- **Numbered lists** are exported as one list, so numbering no longer restarts at 1 on every item.
- **Tables** from HTML, Markdown, EPUB and cloud OCR imports are no longer dropped.
- **Cloud OCR rate limits:** a large book no longer fails part-way with "rate limited": parts stay
  within the account's pages-per-minute limit and ScanMaster waits between them, and if a later
  part still fails, the pages already read are kept. Blank pages from a failed OCR are now reported
  instead of silently imported.
- Several Preferences settings that did nothing now work: the Scanning tab, autocorrect, autosave,
  the bundled LanguageTool grammar engine and the keyboard profile.
- Speech: fixed a crash in line/sentence/paragraph navigation and a count mismatch in SAPI tags.
- Preferences > AI "Refresh models" no longer freezes the app; CHM import no longer pins a CPU core.

### Known issues

- Docling sets heading levels from section numbers ("2.1"); in books without numbered sections
  every heading comes out at the same level.
- The RichEdit editor is still available for one release: set the environment variable
  `SCANMASTER_EDITOR=richedit` before starting ScanMaster if the new editor causes problems.

---

## [2.21.6] - 2026-07-27

### Added

- **Help viewer now renders as real HTML via WebView2** instead of a
  hand-built WPF `RichTextBox`. Confirmed with real NVDA testing: headings,
  lists, and list items now navigate correctly, an improvement over the
  previous viewer. All 78 help topics' content is unchanged — a new
  structural renderer converts the existing topic data to HTML, so nothing
  was retyped. This also served as a real-world feasibility test of whether
  NVDA can read WebView2 content hosted in WPF at all (a genuinely open
  question, since public reports vary by hosting framework); it can.

## [2.21.5] - 2026-07-26

### Fixed

- **v2.21.4's image fix was incomplete for portrait images** — which is the
  common shape for a book illustration, and the exact shape originally
  reported, so that release very likely did not fix the reported problem.
  v2.21.4 scaled a pasted image to fit the editor's *width* but capped its
  *height* at a fixed 1400px constant unrelated to the actual viewport, so a
  900×2400 source still embedded at 525×1400 inside a 486px-tall editing
  area — leaving exactly the oversized-image caret dead zone it was meant to
  remove. Images are now scaled to fit the viewport in **both** axes,
  preserving aspect ratio.

### Added

- **An automated regression guard for the oversized-image bug**, in the
  RichEdit spike suite: it embeds images across seven size/aspect cases
  (8×8 through 2500×3200 and a pathological 300×5000) and asserts none is
  embedded larger than the viewport. Two things this guard did that matter
  more than its passing: it was validated by deliberately disabling the
  scaling fix and confirming it *fails* (an earlier version of the guard,
  built on measuring rendered layout via `EM_POSFROMCHAR`, passed even with
  the fix completely off, because that message clamps at the viewport edge —
  so it was thrown away rather than trusted), and it is what caught the
  incomplete portrait-image scaling above. The pre-existing image test used
  an 8×8 bitmap, far too small to ever expose this class of bug.

## [2.21.4] - 2026-07-26

### Fixed

- **NVDA still didn't announce embedded images even after v2.21.3**,
  despite v2.21.3's UIA fix being verified correct at the raw API level.
  Root-caused this session by comparing two navigation paths at the exact
  same real image location in a real book: TOM's own `Range.Move` to the
  image's paragraph worked correctly, but a genuine simulated Down-arrow
  keypress got permanently stuck on the line immediately before the image
  and could never reach it. A screenshot at that location showed why —
  images were being pasted at their full native pixel resolution with no
  scaling, so a picture could render far taller than the entire visible
  editing pane, which breaks RichEdit's vertical-line hit-testing for
  Up/Down-arrow navigation. Since NVDA only announces content the caret
  actually stops on, it never had a chance to, regardless of how correctly
  the image was exposed to UIA. Fixed by scaling every pasted image to fit
  the editor's actual width (with a sensible height cap) before embedding
  it, so no image's line can become an arrow-key dead zone.

## [2.21.3] - 2026-07-26

### Fixed

- **NVDA never announced embedded images at all**, a real regression from
  the native-RichEdit editor migration (the old WPF editor's real `Image`
  controls did announce them). Root-caused by fetching NVDA's own source
  this session (`UIATextInfo._getTextWithFieldsForUIARange`): NVDA
  discovers embedded pictures during Say-All/browse-mode reading by
  calling `ITextRangeProvider.GetChildren()` on the text range being
  read — a method that was a hard stub always returning an empty array,
  so NVDA had no way to ever discover an image was there, regardless of
  alt text. Now implemented for real: scans the range for RichEdit's
  embedded-object placeholder character and exposes each one as a real
  `ControlType.Image` UIA element carrying its alt text as the Name.
  Verified end-to-end through the actual UIA client API (the same
  interface NVDA itself uses) against a real EPUB: `GetChildren()`
  correctly found all 11 embedded images with their real captions (e.g.
  "Figure 1.1 – LLM Context Window...").

## [2.21.2] - 2026-07-25

### Fixed

- **EPUB images could silently vanish with no indication they were ever
  there.** Confirmed via a real log ("Failed to open clipboard for image
  insertion (Win32 error 0)"): embedding an image into the document uses
  a clipboard round-trip, and `OpenClipboard` can fail transiently (a
  clipboard manager, Windows' own clipboard history, or even another
  thread briefly holding it) — when it did, the whole image block was
  silently dropped, leaving neither a visual nor an accessible trace it
  had ever existed. Two fixes: `OpenClipboard` now retries a few times
  with a short backoff before giving up (most failures are a few
  milliseconds of contention), and if it still fails, the image degrades
  to a real, readable "[Image: ...]" text placeholder (carrying the alt
  text if there is any) instead of vanishing — same instinct as the
  existing "[Table could not be loaded]" fallback for tables.
- **View ▸ Both could wrap text to one character per line.** The
  scanned-page-image side panel reserved a fixed 350px regardless of
  window size; measured via UIA at just 246px of remaining editor width
  on a modest window, and on a narrower one the fixed reservation can
  starve the editor down to a sliver. The image panel is now
  proportionally (star-) sized against the editor column instead of a
  fixed pixel width, with a minimum width on the editor as a backstop.

## [2.21.1] - 2026-07-25

### Fixed

- **Fatal crashes could lose their own stack trace from the log.** The
  logger writes on a background thread for normal throughput, but on a
  crash that terminates the process (`IsTerminating=True`), the CLR tears
  the process down essentially as soon as the crash handler returns —
  there was no guarantee the background writer thread got scheduled in
  time to actually write and flush the exception details just queued,
  so real crashes could show only a bare header line with the stack
  trace silently lost (confirmed via a real crash report where exactly
  this happened). The crash handler now forces a synchronous drain and
  flush before returning, matching the guarantee the normal graceful-exit
  path already had via its own explicit shutdown call.

## [2.21.0] - 2026-07-25

### Added

- **Effect presets.** Speech Settings and Document Elements now offer a
  named-preset picker (enable + choose a preset by name) for 8 voice
  effects instead of raw parameter sliders: Reverb, Echo, Compression,
  and 5 new effects — Chorus, Distortion, Flanger, Gargle, and a 3-band
  Equalizer. Each preset's actual parameters are edited in a new
  Preferences &gt; Effect Presets page (full create/edit/delete, every
  parameter exposed), and are resolved fresh each time speech plays — so
  editing a preset immediately changes every profile/style that
  references it by name, not just new ones. Ships with a starter set of
  named presets per effect (Reverb: Small Room/Large Room/Hall/Church/
  Stadium, and similar sets for the other 7).
- New real DSP for the 5 new effects (Chorus/Flanger share an LFO-
  modulated delay line; Distortion is gain-driven waveshaping; Gargle is
  LFO amplitude modulation; the Equalizer is a 3-band shelf/peak filter
  built on NAudio's own BiQuadFilter), chained in pedalboard order
  (Compression → Distortion → Gargle → Flanger → Chorus → Equalizer →
  Echo → Reverb) alongside the existing Reverb/Echo/Compression.

### Fixed

- **Auto-update could get permanently stuck if a document had unsaved
  changes.** The update helper only waits 10 seconds for ScanMaster to
  exit before swapping files; if the ordinary "Save before exiting?"
  prompt was still waiting on the user at that point, the helper tried
  to rename the still-open app folder and failed outright. The update
  flow now resolves unsaved changes itself, before the download/hand-off
  even starts, so there's nothing left to block the exit afterward. The
  update helper's own folder-rename step also now retries with backoff
  instead of failing on the first transient file lock.
- **"Test Voice" in Speech Settings never reflected the Output Device,
  Pan, or Effects sliders.** It used a separate, un-redirected playback
  path (a private `SpeechSynthesizer.Speak()` call for SAPI5) that never
  touched the shared audio pipeline those settings actually apply to —
  so testing a setting there was silently meaningless, even though real
  document reading already honored it correctly. Test Voice now plays
  through the same pipeline real speech uses.
- **Reverb/Echo/Compression sliders needed ~10 arrow-key presses to move
  one percent.** They were the only sliders in Speech Settings missing
  `TickFrequency`, so keyboard steps didn't align to whole units.

## [2.20.0] - 2026-07-25

### Added

- **Audio output device (soundcard) selection for all speech engines**,
  with a stereo pan control. Available in Speech Settings, persisted per
  speech profile, with automatic fallback to the system default device if
  the saved one is no longer present (unplugged, disabled).
- Real architecture change behind this: every speech engine (SAPI5,
  WinRT, Supertonic, Kokoro, Piper) now plays audio through a new shared
  NAudio/WASAPI-based `AudioOutputManager` instead of talking to hardware
  directly. For SAPI5 specifically (whose .NET API has no device-
  selection support at all), this uses the same technique NVDA's own
  SAPI5 driver uses: audio is captured into a buffer instead of played
  directly, then played back through the shared pipeline, with real
  per-word bookmark timing re-derived from actual playback position.

### Fixed

- **Rapid Stop-then-Start could leave SAPI5 speech stuck reading only one
  word.** A chunk's synthesis, pre-started to overlap with the previous
  chunk's playback, could be left orphaned by a Stop() call and complete
  asynchronously after a brand-new pipeline had already started — its
  stray completion handler would prematurely finalize the new pipeline's
  first chunk. Fixed by properly awaiting any orphaned in-flight
  synthesis before releasing the pipeline's lock, the same fix already
  used for the identical class of race in the Supertonic/Kokoro/Piper
  engines.

## [2.19.4] - 2026-07-25

### Fixed

- **Crash opening some DOCX/EPUB documents.** Two real, distinct causes
  found via real crash logs and fixed:
  1. EPUB import used the strict default of the underlying EPUB library,
     which throws on common real-world non-compliance (e.g. an EPUB 2
     cover `<meta>` referencing a manifest item ID that doesn't actually
     exist). Switched to the library's RELAXED tolerance preset.
  2. A table in a DOCX could make RichEdit's native table-insertion COM
     call throw an unhandled `COMException`, crashing the entire app
     (confirmed via two independent real crash reports with identical
     stack traces). Now caught and degraded to a "[Table could not be
     loaded]" placeholder instead, with a defense-in-depth catch around
     the whole document-loading loop so no single malformed block can
     take down the app again.
- **Speech going permanently silent after a rapid Stop-then-Start.** A
  silently-cancelled synthesis pipeline (from a real race between the
  robust multi-stage Stop and a following Start) never notified the UI,
  leaving it stuck thinking speech was still active. Fixed to correctly
  reset on any non-successful outcome, without disturbing a genuinely
  newer, still-playing request.
- **Voice/engine/rate changes made in Preferences silently reverted on
  restart.** Preferences and Speech Settings disagreed about which store
  is authoritative for the active voice; Preferences now updates the same
  active speech profile Speech Settings does.

## [2.19.3] - 2026-07-25

### Added

- **14 new in-app help topics** for real, shipped features that had no
  documentation reachable from F1/Help: System Requirements, Browse Mode
  (Ctrl+Shift+`, H/T/L/Q/G/1-6 quick navigation), Plugin Manager (neural
  voice downloads), Sort Lines, Footnotes and Endnotes, Table of Contents
  insert, Equations, Borders and Shading, Tab Stops, Document Language,
  Page Setup and Printing, and Batch/Split Convert. Also expanded the
  existing Formatting Text topic to cover text colour/highlight, change
  case, and symbol insert.
- Discovered along the way: `help/*.html` (including the previously-added
  `system_requirements.html`) is never opened by the running app — only
  `CHANGELOG.md` from that folder is read, for Release Notes. The real
  help surface users reach via F1 is `HelpDialog.xaml.cs`'s own topic
  tree, which is what actually got the new content.

## [2.19.2] - 2026-07-25

### Fixed

- **Keyboard focus now lands reliably in the document editor**, fixing
  three distinct, real bugs found via diagnostic logging (not guesswork):
  1. On startup, `FocusActiveEditor()` could call the native focus API
     before the RichEdit control's underlying native window had actually
     been built, silently doing nothing — it now waits for the control's
     real `Loaded` event when that happens.
  2. Leaving the main menu (Escape, or executing a command), and a menu
     command that opens a dialog (e.g. Help > Check for Updates) closing,
     could both leave focus nowhere useful — WPF's own default focus
     restoration has no reliable memory of the native-hosted editor ever
     having been focused. A guarded safety net now restores focus to the
     editor in both cases, without stealing focus from a genuine click
     elsewhere.
  3. Something (confirmed via logging to be WPF's own internal focus
     machinery, not another pane) was found repeatedly stealing native
     focus away from the editor for a couple of seconds after every
     explicit focus request. A bounded retry (not an unconditional
     background loop — an earlier attempt at that was caught fighting an
     unrelated recurring focus source and reverted before shipping) now
     reliably wins that race.
- **F6/Shift+F6 pane cycling** no longer desyncs from what's actually
  focused, and no longer wastes cycle presses on toolbars/panels hidden
  via Preferences.

## [2.19.1] - 2026-07-18

### Fixed

- **Real named-style and heading-level announcement now works with NVDA.**
  Fixed a cross-thread COM safety gap in the custom UIA text provider:
  every provider method called straight into RichEdit's TOM COM interface
  with no thread marshaling, but NVDA queries the provider from its own
  background UI Automation thread, not the app's UI thread. Confirmed with
  real NVDA testing — heading level and named style are now announced
  correctly for the first time since the native RichEdit editor rewrite in
  2.19.0.
- **Tab now inserts a tab character in the document editor** instead of
  doing nothing. WPF's window-hosting layer was silently claiming the Tab
  key for its own keyboard navigation before the native RichEdit control
  ever saw it. Shift+Tab now correctly removes a preceding tab character
  instead of inserting a second one.
- Removed a redundant, racing startup focus call that could occasionally
  leave initial keyboard focus somewhere unexpected.

## [2.19.0] - 2026-07-13

### Changed

- **The document editor is now a native RICHEDIT50W (msftedit.dll) control,
  replacing WPF's `RichTextBox`/`FlowDocument` entirely.** This is the
  editor's core text-rendering rewrite referenced as a "follow-up" in
  2.18.2's style-announcement note. It fixes two long-standing, architecture-
  level limitations that could not be patched around in the old editor:
  - **Real `StyleName` UIA exposure.** NVDA's own "Report style" setting can
    now gate named-style announcements directly, instead of the old
    caret-driven manual notification workaround (which always announced,
    ignoring that setting because WPF's `RichTextBox` had no extension point
    for a custom `UIA_StyleNameAttributeId`).
  - **Huge-document performance.** A 700-page/150,000-block document that
    took the old `FlowDocument`-based editor several minutes to load now
    loads in about 3 seconds. The huge-document auto-downgrade-to-single-page
    workaround is removed; continuous mode handles documents of any size.
  - Feature parity was carried across for formatting (bold/italic/underline/
    strikethrough/color/highlight/font/heading levels/named paragraph
    styles/alignment/indents), images (insert, alt text), tables, footnotes/
    endnotes, lists, page breaks, Find/Replace, Autocorrect, Spell Check,
    Grammar Check, Say-All speech with per-style voice profiles, and
    Accessibility Templates (Low Vision/Dyslexia/High Contrast/Screen
    Reader) — the last of these is now a real, undoable formatting edit
    rather than a purely cosmetic view setting, since RichEdit has no
    view-only font/color concept the way `FlowDocument` did.
  - The old `ScanMasterRichTextBox`/`RichTextBox` editor and its automation
    peer have been removed from the codebase entirely.

### Fixed

- Character-run formatting (strikethrough, text color, highlight, custom
  font/size) is now preserved on load and save — previously silently
  dropped, which was a real risk for documents imported from DOCX with
  colored or highlighted text.
- Several editor-adjacent commands (heading-level navigation, quoted-text
  navigation, Go To Line, Sort Lines, Insert Comment, F6 pane cycling to the
  editor, and keyboard focus after opening/appending a document) are fixed;
  each had silently stopped working during the editor migration.
- Named character/linked styles can be applied again (previously blocked
  with a "not supported yet" message); the style's formatting is applied
  directly, though — unlike paragraph styles — the style's name itself
  doesn't survive a save/reload, only its visual effect.

## [2.18.2] - 2026-07-11

### Fixed

- **Speech stopped working after Stop, requiring an app restart** — the
  three-stage `RobustSpeechStopper` (Stop → Stop → Reset) awaited every step
  with `ConfigureAwait(false)`, so whenever escalation actually reached
  Stage 3 (a real, previously-documented race where SAPI5/WinRT/Supertonic
  ignore the first Stop mid-prompt), `Sapi5Engine.Reset()` ran on a random
  thread-pool thread instead of the UI thread. `SpeechSynthesizer` wraps a
  COM STA object that must be created on the same STA thread that owns it;
  recreating it off-thread left the synth silently broken, so every Speak
  call afterward did nothing until the app was restarted. Fixed by removing
  `ConfigureAwait(false)` throughout `RobustSpeechStopper`, so Stage 3
  always runs on the UI thread that called Stop.
- **Style announcements interrupted NVDA's own speech** — the caret-driven
  named-style notification used `AutomationNotificationProcessing.MostRecent`,
  which tells NVDA to cut off whatever it's currently saying (Say-All output,
  typed-character echo, etc.) to speak the style change immediately. Changed
  to `CurrentThenMostRecent` so it queues behind in-progress NVDA speech
  instead of overwriting it. Note: this still can't honour NVDA's own
  "Report style" formatting-change setting, because WPF's `RichTextBox`
  doesn't expose a UIA `StyleName` text attribute the way Word's document
  does for NVDA to gate on — true parity would need a custom
  `ITextRangeProvider`; documented as a follow-up.

## [2.18.1] - 2026-07-08

### Fixed

- **Crash when Piper is reading and the caret is moved** (arrow keys, Home/End,
  Page Up/Down) — a cancelled speech pipeline could leave its background
  synthesis task still running after the next speak request already
  acquired the lock and started reloading the voice model. Since each
  Piper voice is its own ONNX model file (unlike Supertonic/Kokoro, which
  keep one shared model loaded and only swap a small per-voice style
  vector), a voice change disposes and recreates the whole inference
  session — the orphaned task could then be caught mid-synthesis on a
  session that had just been disposed out from under it, corrupting
  native memory. Reproduced reliably with a stress test (alternating
  voices under rapid interrupt/restart) before the fix and confirmed
  clean after. Root-caused via Windows Event Log crash records
  (`coreclr.dll`, `STATUS_ACCESS_VIOLATION`) pointing at `ScanMaster.exe`.
  The same latent race existed in Supertonic and Kokoro's engines too
  (copied from the same template) and is fixed there as well, even
  though their different model-loading design made it far less likely to
  trigger in practice.
- A related but separate defect in the same code path: cancelling a
  speech request while it was still queued waiting for its turn to
  speak could throw an exception with nowhere to be caught, which is
  fatal if the caller is a WPF key-handler (they must be `async void`).
  Fixed in all three engines.
- All espeak-ng (Piper's phonemizer) calls now run on one dedicated
  background thread for the life of the process, instead of whichever
  .NET thread-pool thread happened to be free — closes a possible
  thread-affinity issue in the native library that a lock alone
  wouldn't have prevented.

---

## [2.18.0] - 2026-07-07

### Added

- **Piper Neural TTS is now a fully working speech engine** — available for
  both live reading and audio export, using the same on-demand Plugin
  Manager download pattern as Supertonic and Kokoro. Phonemization uses
  espeak-ng's public C API directly (its GPL-3.0 runtime is a separate,
  optional download — never compiled into ScanMaster's MIT-licensed
  installer); voice synthesis runs through ONNX Runtime, already used
  elsewhere in the app. The engine addon (~171 MB) bundles espeak-ng plus
  one starter voice (Lessac, US English, high quality); 28 more
  single-speaker English voices (7 originally, 21 added from the full
  rhasspy/piper-voices catalog — see the project memory for the complete
  list) are available individually via the Plugin Manager. Multi-speaker
  voice packs (VCTK, LibriTTS, Arctic, and similar large collections) are
  intentionally not included — they'd need a per-speaker picker UI that
  doesn't exist yet.
- Plugin Manager's `AddonManager` gained zip-extraction support (needed for
  espeak-ng's ~440 small dictionary files) — a downloaded zip can now
  extract into an addon's folder instead of being installed as a single
  file, without changing how installed-status is checked.

### Known limitations

- The stock espeak-ng Windows DLL doesn't export the newer
  terminator-aware phonemization function, so mid-sentence pauses at
  commas/semicolons/colons can occasionally be absorbed rather than
  producing an audible pause — sentence-ending punctuation (periods,
  question marks, exclamation points) is unaffected. Pronunciation
  correctness is not affected either way.

---

## [2.17.0] - 2026-07-06

### Added

- **Kokoro Neural TTS is now a fully working speech engine** — available for
  both live reading (Preferences ▸ Speech, Speech Settings) and audio
  export, with 54 voices across US/GB English. Downloads on demand via the
  Plugin Manager (~354 MB: the ONNX model plus voice styles), same as
  Supertonic. Unlike typical Kokoro integrations, this doesn't depend on
  Docker or espeak-ng: ScanMaster bundles its own from-scratch English
  phonemizer (a C# port of the misaki project's dictionary-based G2P
  algorithm) so the whole pipeline runs in-process.

### Known limitations

- Part-of-speech tagging (used to disambiguate pronunciations like "read"
  as present vs. past tense) is a rule-based approximation rather than a
  full statistical tagger, so heteronyms may occasionally mispronounce.
  Unknown proper nouns are skipped rather than spelled out phonetically.

---

## [2.16.1] - 2026-07-06

### Fixed

- **Supertonic download failed with "The SSL connection could not be
  established"** on networks that block `huggingface.co` (confirmed via a
  user report — the site was unreachable even from a web browser on their
  machine, not just ScanMaster). Supertonic's model files now download
  from a GitHub-hosted mirror instead, verified byte-identical to the
  original via the same pinned SHA-256 hashes. Also: download-failure error
  dialogs (Plugin Manager and the Preferences ▸ Speech download prompt) now
  show the actual underlying error instead of a generic, unhelpful message.

---

## [2.16.0] - 2026-07-06

### Added

- **Plugin Manager** (`Tools ▸ Plugin Manager…`): a new, generic dialog for
  downloading optional speech engines instead of bundling everything in the
  installer. Built to be expandable to non-speech addon categories later.
- **Supertonic Neural TTS is now a Plugin Manager download** instead of an
  installer component — the installer and portable zip are both ~415 MB
  smaller. The existing "download Supertonic" prompt in Preferences ▸
  Speech still works, now routed through the same shared download code.
- Kokoro's model files can be downloaded via the Plugin Manager as a first
  step toward future Kokoro support. This does not add a working voice yet
  — see Known limitations below.

### Changed

- Supertonic's model-download logic moved from a one-off downloader class
  into a generic, reusable addon-install framework
  (`ScanMaster.Core/Addons`), shared by every current and future
  downloadable engine.

### Known limitations

- Kokoro and Piper are listed in the Plugin Manager but not yet functional.
  Kokoro needs a text-to-phoneme step (misaki or espeak-ng) that isn't
  wired into ScanMaster yet; Piper needs a native library that isn't built
  yet. Both are tracked for a future release.

---

## [2.15.47] - 2026-07-06

### Fixed

- **NVDA still didn't announce named styles while navigating with arrow
  keys**, even with "report style changes" enabled. The v2.15.45 fix
  correctly restored the invisible per-paragraph style label, but that
  label is only ever spoken by NVDA in Say-All mode, not during ordinary
  caret navigation, which relies on an explicit UIA notification. Named
  style changes now raise a UIA notification directly (the same
  `RaiseNotificationEvent` mechanism already used for the global spacebar
  fix), so NVDA speaks the style immediately as the caret moves. Headings
  are unaffected (still announced natively via heading-level exposure, no
  double-announcement).
- **Ctrl+Shift+S "Apply Style" combo did nothing on Enter.** Arrowing to a
  style in the open dropdown and pressing Enter closed the dropdown but
  never applied the style or returned focus to the editor — WPF's
  `ComboBox` swallows Enter internally while its dropdown is open, before
  the app's own key handler ever saw it. The handler now runs on
  `PreviewKeyDown` (tunnelling, so it gets first refusal) instead of the
  bubbling `KeyDown`, and reliably applies the selected style and returns
  focus to the document.
- **Word count in the status bar didn't reset when switching or closing
  documents** — it only updated on the next keystroke, so opening a new
  document after a large one showed the old document's stale count until
  you typed. The count now recomputes immediately whenever the active
  document tab changes.

---

## [2.15.46] - 2026-07-04

### Fixed

- **Audio export could fail with a bare "Object reference not set to an
  instance of an object"** when using an active per-style speech profile.
  The v2.15.44 parallel-rendering change resolved each block's voice by
  calling the caller's resolver from multiple worker threads at once; when
  a per-style profile is active, that resolver queries `PreferencesDb`,
  which holds a single shared SQLite connection — concurrent access
  corrupted it sporadically. Every block's voice is now resolved up front,
  single-threaded, before rendering starts, removing all concurrent
  database access.
- **Audio export could crash the whole application outright** on
  lower-spec machines (confirmed on a 16 GB / Core i5 machine) when using
  the Supertonic engine. Parallel rendering gave every engine one renderer
  instance per worker thread — cheap for SAPI5/WinRT, but Supertonic loads
  several ONNX models per instance (hundreds of MB to a few GB), so
  multiple concurrent instances exhausted memory and crashed hard enough
  to bypass .NET's own exception handling entirely (confirmed via a log
  that ended mid-startup with no error ever recorded). Supertonic now uses
  exactly one shared, lock-serialized renderer instance for the whole
  export regardless of parallelism degree; SAPI5/WinRT keep full per-worker
  parallelism.

---

## [2.15.45] - 2026-07-04

### Fixed

- **NVDA stopped announcing named paragraph styles** (Quote, Code, Title,
  etc. — anything other than a heading or "Normal"). Root-caused to a
  v2.11.8 regression: that release removed the invisible screen-reader-only
  label ScanMaster prepends to each paragraph ("`<StyleName>. `") on the
  reasoning that headings were already announced correctly via the
  RichTextBox's `AutomationPeer` heading-level exposure — true for
  headings, but WPF has no other mechanism to expose arbitrary named
  styles to NVDA, so removing the label silently killed announcement for
  everything that isn't a heading. Restored the label for non-heading
  named styles in both the paginated editor
  (`ScanMasterRichTextBox.BuildParagraph`) and the continuous view
  (`DocumentView.BuildFlowParagraph`) — headings remain untouched (still
  handled via the AutomationPeer only, avoiding the double-announcement
  that the v2.11.8 fix originally addressed).

---

## [2.15.44] - 2026-07-04

### Added

- **Parallel block rendering for audio export.** Blocks were previously
  rendered strictly one at a time regardless of priority — "Normal" just
  meant "no throttling," not "use available CPU." Now Normal renders
  using about half your CPU cores, High/VeryHigh use all of them (VeryLow/
  Low stay sequential, unchanged, since those tiers exist to keep the
  machine responsive rather than go fast). Rendering happens in bounded
  batches independent of book length, so a 584-page (or longer) book with
  no heading structure still has bounded memory use, and output order is
  always reconstructed to match the old sequential result exactly.
  Supertonic's ONNX thread budget is divided across parallel workers to
  avoid oversubscribing the CPU.
- **Selectable log verbosity + timing instrumentation.** Preferences ▸
  Advanced's debug-logging checkbox is now a 4-level combo: No logging /
  Info (default) / Debug / Input-Output (verbose). Input/Output mode logs
  per-block render timing, chapter totals, and segment-flush timing during
  audio export, so a slow export can be diagnosed from `scanmaster.log`
  instead of just looking stuck. The saved log level is now applied from
  the very first line at startup (previously silently ignored until
  Preferences was opened once in a session).

### Fixed

- `WinRtRenderer` re-scanned every installed voice on every single block
  even when the voice hadn't changed (unlike `Sapi5Renderer`, which
  already cached). Fixed — matters more now that it runs `Degree` times
  concurrently.

---

## [2.15.43] - 2026-07-02

### Fixed

- **Audio export rendered at the wrong (much slower) speed.** All three
  offline renderers (`Sapi5Renderer`, `WinRtRenderer`,
  `SupertonicRenderer`) treated the incoming rate as legacy
  words-per-minute, but the caller (`AudioExportSupport.BuildResolver`)
  documents and passes SAPI scale (−10..+10). At the default rate (0),
  SAPI5 exports actually rendered at −8 (very slow); WinRT/Supertonic
  exports always rendered at their minimum speed floor. Fixed all three
  to interpret the value on the documented SAPI scale.
- **WinRT speech engine init failure was silently swallowed**, with no
  logging at all, and permanently cached until app restart — matching a
  report of "didn't start speaking until I relaunched." Now logs the
  actual exception so a future occurrence is diagnosable.
- Added heartbeat logging (every 50 blocks) and per-block error context
  (block index, chapter, engine) to `AudioExporter`, so a stalled or
  failed export on a very large document leaves a diagnosable trace in
  `scanmaster.log` instead of no information at all.

### Added

- **New audio export split mode: "Separate files, every N pages."** For
  documents with no (or unreliable) heading structure, where the
  heading-based split modes collapse into one giant chapter/file. Page
  count is set via a native spinbox (WinForms `NumericUpDown`, hosted
  the same way native list views are elsewhere in the app), defaulting
  to 20 pages per file.

---

## [2.15.42] - 2026-07-02

### Fixed

- **Audio export could pin RAM near 100% and crash with "Arithmetic
  operation resulted in an overflow"** on long documents with no heading
  structure (common for OCR'd scans) or exported with the "Single File"
  split mode. `ChapterPlanner` collapses such documents into ONE chapter
  covering the whole book, and the exporter only flushed rendered PCM to
  disk at chapter boundaries — so for exactly this case, the entire
  book's audio still accumulated in one in-memory buffer before anything
  was written. Once that buffer crossed ~2.1 billion samples, a WAV
  buffer allocation hit a C#-spec quirk (array-size conversions from
  `long` are always overflow-checked) and threw a bare, contextless
  `OverflowException`.
  - `AudioExporter` now flushes to a new temp WAV segment every 10
    minutes of rendered audio, regardless of chapter boundaries, so
    peak PCM in memory is bounded to a few tens of MB no matter how the
    document is structured. Chapters split across multiple segments are
    concatenated via ffmpeg's concat demuxer at encode time.
  - `WavCodec.Resample`/`Write` now throw a clear, descriptive error
    instead of the bare overflow message if an oversized buffer is ever
    fed through in one call.

---

## [2.15.41] - 2026-07-02

### Changed

- **AI Assistant dialog reworked for visibility and editability.**
  - The prompt box is now multiline (wraps, scrolls, grows) instead of a
    single-line box that hid most of what you typed.
  - Opening the dialog with editor text selected now pre-fills the
    prompt box with that selection directly (visible, editable, selected
    so typing replaces it), instead of silently appending it behind the
    scenes at send time. With no selection, the box opens empty as
    before.
  - Quick Action buttons (Summarise, Simplify, etc.) now prepend their
    instruction above the existing box content rather than overwriting
    it — the box is always exactly what gets sent.
  - Added an indeterminate busy indicator and a "Waiting for
    `{Provider}` (`{Model}`)…" status message while a request is in
    flight, so it's clear a Send actually fired instead of looking
    frozen. The Send button disables during the request.
  - Failed requests now turn the status text red in addition to the
    existing error message.
  - **Ctrl+Enter** sends the prompt from anywhere in the dialog; **Esc**
    closes the dialog, including from inside the multiline prompt box.

---

## [2.15.40] - 2026-07-02

### Fixed

- **NVDA read heading / formatted lines twice** in text boxes that
  contained double line breaks. Users reported the "line has two
  linefeeds" symptom in the Dictionary Lookup dialog's Definitions and
  Examples boxes and in the AI Assistant Response box. Root cause: a
  blank line between paragraphs (produced by `\r\n\r\n` or Unix-style
  `\n\n` from an LLM reply) makes NVDA re-announce the previous
  non-empty line as context when the caret lands on the blank one.

  - **DictionaryDialog** — single `\r\n` between senses / examples
    (no blank-line separator); embedded line breaks inside each
    definition or example flattened to a space so a mid-entry `\n`
    can't create a stub second line.
  - **AI Assistant Response box** — LLM replies now run through a
    normaliser that converts every `\n`, `\r`, and `\r\n` to `\r\n`
    and collapses consecutive breaks to a single one, so there is
    never a blank line to double-read.

---

## [2.15.39] - 2026-07-02

### Fixed

- **NVDA+End (report status bar) announced the status bar twice.** The
  per-item `AutomationProperties.Name` attributes added in v2.15.35
  (so arrow-key landing on each `StatusBarItem` would announce
  "Current page" etc.) caused NVDA to enumerate the status bar's
  children when reporting, reading the composed status line AND each
  item's name plus its `TextBlock` text. Removed the per-item Names —
  NVDA+End now reads the composed line once, and arrow-key navigation
  between items reads the focused item's text via its `TextBlock`
  content (still works after v2.15.38's arrow-key trap).

---

## [2.15.38] - 2026-07-02

### Fixed

- **F6 landing on the status bar no longer leaks arrow keys** into the
  Styles combo or the Navigation treeview. The
  `KeyboardNavigation.DirectionalNavigation="Contained"` XAML attribute
  from v2.15.35 wasn't holding for the `StatusBar` subclass, so Left
  and Right still escaped. `AccessibleStatusBar` now intercepts
  Left / Right / Home / End in `PreviewKeyDown`, walks between its six
  `StatusBarItem` children programmatically, and marks the event
  handled so nothing else sees it. Up / Down are hard-consumed with
  no movement. Ctrl/Alt/Windows modifiers pass through untouched so
  real shortcuts still work.

---

## [2.15.37] - 2026-07-01

### Fixed

- **Auto-updater now refuses to start on a full disk** with a clear
  message ("Not enough free disk space… need 2.85 GB, only 640 MB
  available") instead of silently hanging partway through extraction.
  The pre-flight check sums the update zip's uncompressed entries plus
  10 % headroom and compares against the target drive's free space
  before touching anything, so the existing installation stays intact.

- **Update dialog no longer appears at startup when the current
  version is already the latest.** Belt-and-braces version comparison
  at the display site normalises both current and release versions
  to 4-part form and suppresses the dialog if `release <= current`,
  guarding against any version-parse quirk in the checker.

---

## [2.15.36] - 2026-07-01

### Fixed

- **Auto-updater silently stalled with only a Close button visible.**
  When the swap failed with an exception whose `Message` was blank (or
  before the UI could switch to the error state), the progress window
  ended up showing just the Close button with no headline text. Every
  stage of the swap now writes to a diagnostic log at
  `%TEMP%\scanmaster-update-<timestamp>.log`, the error dialog always
  composes readable text even when the exception has no message, and
  the inner-exception cause is surfaced too. The most common
  root-cause (installed under Program Files, updater not elevated,
  Directory.Move on `app\` fails with "Access is denied") now surfaces
  a targeted message explaining exactly what happened.

  Note: the fix ships in this version's helper, so it takes effect for
  the v2.15.36 → v2.15.37 upgrade path. Users hitting the silent stall
  on the v2.15.35 → v2.15.36 upgrade should download the installer or
  portable zip from the release page and install manually.

---

## [2.15.35] - 2026-07-01

### Added

- **Standard toolbar split out from Formatting toolbar.** Standard now
  carries New / Open / Save / Cut / Copy / Paste / Select All / Undo /
  Redo; Formatting keeps Bold / Italic / Underline, the Style picker,
  and Zoom. Each is togglable independently from View ▸ Toolbars.
- **Free-model indicator** in the Preferences ▸ AI models combo. Models
  we can confidently identify as free-to-use (OpenRouter `:free` tag,
  every local Ollama model) render with a trailing "— free" and the
  refresh-status line reports the count ("Loaded 45 model(s) (12 free)").
  The suffix is display-only and stripped before hitting any provider.

### Fixed

- **Page-list sidebar stuck the status bar on "Page 1"** when the user
  double-clicked / pressed Enter on a later page. The activation handler
  called `NavigateToPage` directly instead of routing through
  `GoToPage`, so the status bar update, sidebar reselection, slider
  refresh, and speech resume never fired until the next arrow-key
  press. Now uses `GoToPage`.
- **Navigation treeview Enter didn't move the editor or update the
  status bar.** `OutlinePanel.Navigate` now fires a `PageNavigated`
  event; MainWindow subscribes and refreshes the status bar, page
  sidebar selection, and slider, so arrow-key browsing AND Enter both
  keep the rest of the window in sync with the outline-driven jump.
- **F6 → status bar leaked arrow-key navigation into the Styles pane.**
  Status bar now uses `DirectionalNavigation=Contained` +
  `TabNavigation=Once` so Left/Right walk only its six items (Page,
  Line/Col, Style, Words, Speech, File); each item is `Focusable` with
  an accessible name so NVDA announces "Current page, Page 1 of N" etc.
- **Voice rate defaulted to −10 on fresh installs.** The Speech
  Settings dialog was running `WpmToSapiRate(0)` on the migrated
  `prefs.speech_rate` (already on the SAPI scale post-v2.15.11),
  which clamped to −10. Now checks if the stored value is already in
  the SAPI range before running the WPM conversion — default is 0.
- **Refresh models in Preferences ▸ AI** now moves focus onto the
  models combo so the user can pick immediately without groping back.
- **Ollama Cloud / OpenRouter API keys pasted from a password manager
  silently 401'd.** Trailing whitespace / newlines on the pasted key
  turned the request header into `Bearer <key>\n`, and both providers
  reject that with an opaque body. All API keys are now trimmed at
  save time in Preferences AND before each request in every provider.
- **AI Assistant showed "Response received" with a blank Response box**
  when the provider returned an unexpected envelope shape. Both the
  OpenAI-compatible parser (OpenAI, Mistral, OpenRouter) and the
  Ollama Cloud parser now surface the raw response snippet in the
  status line instead of returning "" so the user sees exactly what
  the provider sent back.

---

## [2.15.34] - 2026-07-01

### Added

- **AI thesaurus fallback in Dictionary Lookup.** When the bundled
  WordNet database has no synonyms or antonyms for a word — rare or
  technical or multi-word terms it doesn't cover — the dialog now asks
  the configured AI provider (OpenAI, Anthropic, Gemini, Mistral,
  OpenRouter, Ollama, Ollama Cloud, HuggingFace) for extras and merges
  them into the corresponding tabs. Silent when AI is disabled or
  unconfigured — WordNet still runs first, and offline users get
  exactly what they got before. Design borrowed from Quill's
  `core/ai/thesaurus.py` (pattern, not code — Quill is GPL).

- **Undo change** button in the Spelling dialog. Reverts the most
  recent Change / Change All while the F7 session is still open, so a
  mistaken replacement no longer requires closing the dialog and
  running Ctrl+Z through the editor. For ChangeAll it also drops the
  auto-replace rule so subsequent occurrences of that word are
  re-surfaced rather than silently rewritten.

- **Clear** button in the AI Assistant, next to Send. Empties the
  prompt box in one click and returns focus to it — previously a long
  free-form question required select-all + delete.

### Changed

- **Session-scoped ignore in the Spelling dialog.** "Ignore" now
  suppresses the current word for the rest of the F7 session (matches
  Word). Previously it only skipped past this one hit, so a repeated
  typo re-prompted every occurrence. Permanent additions still go
  through "Add to dictionary".

### Fixed

- **NVDA now announces the spacebar in every editbox.** The
  v2.15.33 attempt only wired the UIA notification into the main
  editor, and WPF's per-control `PreviewTextInput` didn't consistently
  fire for space anyway. Replaced with a single global class handler
  on `TextBoxBase.KeyDownEvent` in `App.OnStartup`, so every TextBox
  and RichTextBox in ScanMaster (editor, dialogs, Find/Replace, spell,
  AI Assistant, everywhere) raises the "space" notification when the
  bare spacebar is pressed in a writable field. Ctrl+Space and
  Alt+Space are treated as chords and don't fire the notification.

---

## [2.15.33] - 2026-07-01

### Added

- **Tools ▸ Thesaurus…** menu entry. The existing `DictionaryDialog`
  already served as a thesaurus (Synonyms / Antonyms / Related tabs) —
  but users searching the menu for "Thesaurus" couldn't find it. The
  new menu item points at the same `DictionaryLookupCommand`, so it's
  discoverable both ways. Dictionary Lookup also gained its
  `Ctrl+Shift+D` gesture hint in the menu.

- **Ctrl+Space adds an autocorrect entry for the word at the caret.**
  Grabs the current selection (if any), otherwise the word left of the
  caret, and opens the Autocorrect dialog with the trigger pre-filled
  and focus on the Replacement box. Registered as
  `tools.autocorrect_add` for Keyboard Manager rebinding.

- **Keyboard Manager audit.** Every menu item is now bindable:
  - Categories sort in menu-bar order (File → Edit → View → Insert →
    Format → Pages → Scan → Speech → Tools → Review → Help), not
    alphabetically (which used to put Edit above File).
  - 14 recently-added commands registered in `FeatureRegistry` —
    `navigate.heading_{1..6}_{next,prev}` (Alt+digit chords),
    `navigate.toggle_browse_mode` (Ctrl+Shift+\`), `review.heading_lint`.
  - 5 menu commands added to both the command map and the registry
    (`file.batch_document_convert`, `file.split_and_convert`,
    `help.quick_start`, `speech.next_page`, `speech.prev_page`).

### Fixed

- **F6 now owns pane switching. Tab no longer escapes non-editor panes.**
  Previously pressing Tab in the page sidebar would move focus to the
  document scrollbar, then to the outline, then eventually into the
  editor where it inserted a tab character. The tunnel-level
  `MainWindow_PreviewKeyDown` now marks Tab / Shift+Tab handled
  whenever focus is not inside a `ScanMasterRichTextBox`, so the user
  stays in the current pane until they press F6 to move. Tab in the
  editor still inserts a tab stop (handled by the editor's own
  `OnPreviewKeyDown` before the intercept fires).

- **NVDA now announces space typing in the editor.** WPF's RichTextBox
  fires `TextChangedEvent` inconsistently for whitespace-only edits and
  NVDA's "speak typed characters" filter often skipped space entirely.
  `ScanMasterRichTextBox.OnPreviewTextInput` now raises a UIA
  `RaiseNotificationEvent` with the string "space" when the incoming
  character is space (only), which NVDA reads. No effect on other
  characters (NVDA handles those natively).

- **Read-only caret invisibility, second pass.** Six more dialogs had
  read-only TextBoxes missing `IsReadOnlyCaretVisible="True"`:
  `AiAssistantDialog.ResponseBox`, `GrammarDialog.TextPreview`,
  `KeyboardManagerDialog.CurrentBindingBox`,
  `KeyCaptureDialog.CaptureBox`,
  `OcrLanguageManagerDialog.TessdataPath`,
  `SapiTagDialog.PreviewBox`. All fixed. Also set unconditionally on
  the editor (`ScanMasterRichTextBox` constructor) so browse mode
  (Phase 5, read-only editor for single-letter Quick Nav) still shows
  a caret.

- **Removed the redundant Ctrl+Space pause-speech binding.** F3 was
  already the primary pause chord; Ctrl+Space duplicated it and now
  serves the autocorrect-add flow above.

---

## [2.15.32] - 2026-07-01

### Added

- **Editor context menu now offers Synonyms and Antonyms** for the word at
  the cursor (from the bundled WordNet 3.x). Right-click — or press the
  Apps key / Shift+F10 — and you get a "Synony_ms" submenu with up to 15
  WordNet alternatives plus an "Anton_yms" submenu. Click any entry to
  replace the word in the editor. A "Thesaurus for \"word\"…" launcher at
  the bottom opens the full Dictionary dialog for richer browsing
  (definitions, examples, broader / narrower terms). Works on
  correctly-spelled words too — not just misspellings.

- **Update helper now shows a WPF progress window** instead of an empty
  console. Status text is a live region (NVDA announces every stage:
  "Waiting for ScanMaster to close…" → "Extracting <file> (N of M)…" →
  "Update complete. Restarting…"), with a determinate progress bar that
  fills during extraction. On failure the window stays open with a
  Close button so the error is readable. `OutputType` switched from
  `Exe` to `WinExe` so no console window flashes.

### Fixed

- **Active speech profile not honoured on restart** (long-standing bug).
  Speech settings lived in two parallel sources of truth: the
  `speech_profiles` table (where the dialog's **Save** button writes)
  and the legacy `prefs.speech_engine` / `prefs.voice` /
  `prefs.speech_rate` / `prefs.speech_volume` keys (where MainWindow
  reads on startup). They only stayed in sync when the user clicked
  **OK**. Clicking **Save** alone left prefs.* stale → next launch
  picked the old voice / rate. MainWindow now treats the active profile
  as authoritative on startup and mirrors its values into prefs.* for
  legacy readers. The dialog's Save AND OK paths both call a new
  `SyncLegacyPrefsToActiveProfile` helper so the two sources can never
  drift again.

- **AI Assistant did not respond when no text was selected** —
  `SendRequestAsync` silently rejected with status "No text selected"
  and the `StatusText` TextBlock had no `LiveSetting`, so screen-reader
  users heard nothing and assumed the Send button was broken. The
  dialog now allows **free-form questions** without a selection (switches
  the system prompt from "writing assistant" to "general assistant"),
  the Replace button is correctly disabled when there's no selection to
  replace, and `StatusText` is a polite live region so NVDA announces
  every state change.

- **Mathpix / Mistral OCR silently returned empty text for every page**
  when the API returned HTTP 200 with an `error` field (image_too_large,
  no_implementation, rate-limit, auth issues). Both engines now throw
  `HttpRequestException` carrying the full provider error message
  whenever `error` is present or `text` is missing. Credentials are
  trimmed on read AND on save (`PasswordBox` doesn't strip trailing
  whitespace, so a credential-manager paste used to invalidate every
  request silently).

- **Update dialog: caret invisible / arrow keys did nothing** in the
  "Current version" and "New version" read-only TextBoxes. WPF hides the
  caret in read-only TextBoxes by default; added
  `IsReadOnlyCaretVisible="True"` to both. Screen-reader users can now
  arrow through the version strings character-by-character.

- **Belt-and-braces against the "helper.exe in use" lock error.** The
  helper detects when it can't overwrite its own running .exe and writes
  to `<dest>.new` instead. The launcher promotes `*.new` files on every
  startup. From v2.15.30 onward this prevents the lock error from
  recurring no matter how some future caller invokes the helper.

---

## [2.15.31] - 2026-07-01

### Fixed

- **Active speech profile not honoured on restart** (long-standing
  bug). Speech settings lived in two parallel sources of truth:
  the `speech_profiles` table (where the Speech Settings dialog's
  **Save** button writes) and the legacy `prefs.speech_engine` /
  `prefs.voice` / `prefs.speech_rate` / `prefs.speech_volume` keys
  (where MainWindow's startup loader reads). They only stayed in
  sync when the user clicked **OK** — clicking **Save** alone
  (then closing the dialog with the **X**) left prefs.* stale, so
  the next launch picked the old voice / rate.

  **Fix in two places:**

  - `MainWindow` now treats the active profile as authoritative on
    startup. Reads `_prefs.GetActiveSpeechProfile()` first; uses
    its engine / voice / rate / volume; falls back to prefs.* only
    when no profile exists (fresh installs). Also mirrors the
    profile values into prefs.* so any code path still consulting
    the legacy keys sees the same settings. Startup log now
    records the source (`Source=profile "MyVoice"` vs
    `Source=prefs`) for verification.
  - `SpeechSettingsDialog`: new `SyncLegacyPrefsToActiveProfile`
    helper called by both `SaveCurrentProfile` (Save button) and
    `PersistActiveProfileFromUi` (OK button), so neither path can
    leave prefs.* out of step with the profile table again.

  Existing installs auto-correct on first launch of v2.15.31 —
  whatever the active profile says is what the engine uses.

---

## [2.15.30] - 2026-06-30

### Fixed

- **Update dialog: caret was invisible / arrow keys did not navigate
  the "Current version" and "New version" read-only TextBoxes.** WPF
  hides the caret in read-only TextBoxes by default; added
  `IsReadOnlyCaretVisible="True"` (matching what `NotesBox` already
  had), so screen-reader users can now arrow through the version
  strings character-by-character.

- **Belt-and-braces against the "helper.exe in use" lock error.** Even
  though v2.15.28's `UpdateInstaller` already copies the helper to
  `%TEMP%` before running it, the helper now ALSO handles the case
  where some future caller (or the legacy v2.15.27 caller still in
  circulation) launches it in-place from the install directory:

  - If extraction encounters a locked `ScanMaster.UpdateHelper.exe`
    (`IOException` and the destination matches our own
    `Environment.ProcessPath`), the new content is written to
    `ScanMaster.UpdateHelper.exe.new` instead of throwing.
  - `ScanMaster.Launcher` (`ScanMaster.exe`) now runs
    `PromoteNewFiles(root)` on every startup — enumerates `*.new`
    files at the install root, deletes the original, and renames the
    `.new` into place. Best-effort; failures leave the original
    intact.

  Net effect: from v2.15.30 onward the auto-updater is robust to
  helper-self-lock regardless of how the caller invoked it.

  **Recovery for users stuck on v2.15.27 portable:** the buggy
  in-place call lives in the *running* app, so the v2.15.30 fix
  cannot reach you remotely. You need a manual upgrade *once*:
  download `ScanMasterSetup-2.15.30.exe` (the installer doesn't use
  the helper) or extract `ScanMaster-portable-2.15.30.zip` over the
  existing folder. After that, auto-updates work for ever after.

---

## [2.15.29] - 2026-06-30

### Added

- **Review ▸ Check Heading Structure…** — accessibility linter for the
  active document's heading sequence. Flags three classes of issue:
  *level skipped* (e.g. H1 → H3 with no H2 in between), *starts above
  level 1* (first heading is H2 or deeper), and *empty heading*
  (heading block with no visible text). Dialog uses the native Win32
  ListView with columns Page / Level / Issue / Title. Enter or
  double-click jumps the editor to the offending heading; the dialog
  stays open so the user can walk through every issue without
  re-opening it. Borrowed from Quill's `markdown_sections.py`.

- **Heading-level navigation shortcuts** — surface the existing
  `NavigateByHeadingLevel` method as direct keyboard chords:
  - **Alt+1 … Alt+6** → next heading at that level.
  - **Alt+Shift+1 … Alt+Shift+6** → previous heading at that level.
  Also exposed as a **Pages ▸ Navigate by Heading** submenu and as 12
  named commands (`navigate.heading_{1..6}_{next,prev}`) so Keyboard
  Manager users can rebind. WPF's `InputBinding` system captures
  these before menu activation, so typing digits in the editor is
  unaffected.

- **Browse mode** (Quill-style Quick Nav) — toggle with
  **Ctrl+Shift+`** or **View ▸ Browse Mode**. While on, the active
  editor goes read-only and bare letter keys navigate elements:

  | Key | Element |
  | --- | --- |
  | `H` | next/prev heading (any level) |
  | `1`–`6` | next/prev heading at that level |
  | `T` | next/prev table |
  | `L` | next/prev list |
  | `Q` | next/prev quote |
  | `G` | next/prev graphic / image |

  Shift+letter reverses direction. Status-bar live region announces
  the mode change so screen readers confirm entry/exit. Tab switching
  preserves the browse-mode state across editors.

---

## [2.15.28] - 2026-06-30

### Fixed

- **Portable auto-update failed with "The process cannot access the
  file 'ScanMaster.UpdateHelper.exe' because it is being used by
  another process."** Classic self-update bootstrap problem: the
  helper was launched in-place from the install directory and then
  tried to unzip a new portable bundle (which contains a fresh
  `ScanMaster.UpdateHelper.exe`) on top of itself — Windows refuses
  to overwrite a running .exe.

  **Fix:** `UpdateInstaller.RunPortableAsync` now copies the helper
  to `%TEMP%\ScanMaster.UpdateHelper.<version>.exe` and launches
  that copy instead. The install-directory helper is no longer
  locked, so the new zip overwrites it cleanly.

  *Recovery for v2.15.22-v2.15.27 portable users:* the buggy
  updater is in the *running* app, so you need a manual upgrade
  once to get past it — either run `ScanMasterSetup-2.15.28.exe`
  (the installer route doesn't use the helper) or extract
  `ScanMaster-portable-2.15.28.zip` over your existing folder.
  From v2.15.28 onward auto-update works.

---

## [2.15.27] - 2026-06-30

### Fixed

- **Mathpix OCR silently returned empty text for every page**, causing
  whole-book imports (e.g. a 203-page STEM textbook) to produce a
  document of completely blank pages with no diagnostic. Root cause:
  Mathpix's `v3/text` endpoint does NOT use HTTP status codes for
  most failures — it returns HTTP 200 with `{"error": "...",
  "error_info": {...}}` for things like `image_too_large`,
  rate-limit, auth problems, and `no_implementation`. The engine's
  `TryGetProperty("text", …) ?? ""` pattern dropped those errors and
  handed the importer an empty string per page, so the importer's
  exception-based per-page error capture (`firstOcrError`) was never
  triggered.

  **Fix:** `MathpixOcrEngine` now throws `HttpRequestException` with
  the full Mathpix error message when the response has an `error`
  field or when `text` is missing/null. The same defensive pattern
  was applied to `MistralOcrEngine` (which had the same shape of
  silent failure). Next time an OCR import fails, the actual reason
  shows up in the document description and `ocr_debug.log.enc`,
  e.g. `Mathpix error: image_too_large {...}`.

- **Cloud OCR credentials are now trimmed on save and on read.**
  `PasswordBox` does not strip trailing whitespace; a copy-paste
  from a credential manager (or a pasted line with a trailing
  newline) would silently break every Mathpix/Mistral request. The
  Preferences ▸ Cloud OCR save path now trims all five credential
  fields, and the Mathpix + Mistral engines also trim on read for
  belt-and-suspenders.

---

## [2.15.26] - 2026-06-30

### Fixed

- **v2.15.25 launcher refused to start when installed *over* an earlier
  version.** The new single-file launcher's bundled .NET host was
  picking up the orphaned `hostfxr.dll` / `coreclr.dll` /
  `ScanMaster.runtimeconfig.json` left behind in the install root by
  v2.15.22-v2.15.24 (the installer overwrote files but never deleted
  obsolete ones). Inno Setup now has an `[InstallDelete]` block that
  removes every loose `.dll` plus `ScanMaster.deps.json`,
  `ScanMaster.runtimeconfig.json`, and `createdump.exe` from the
  install root *before* copying the new files, so the launcher's
  bundled runtime is the only one in the directory.

  *Recovery for users already stuck on v2.15.25:* run the v2.15.26
  installer — it cleans the orphans automatically. Portable users
  should extract `ScanMaster-portable-2.15.26.zip` to a **fresh
  folder** (or first delete all loose `.dll` files plus the
  `ScanMaster.deps.json` / `ScanMaster.runtimeconfig.json` /
  `createdump.exe` from the existing folder), then copy across
  `scan_master.db`, `portable.marker`, and any `.log` files you
  want to keep.

---

## [2.15.25] - 2026-06-30

### Fixed

- **Portable auto-update broken: `MissingMethodException` in
  `ScanMaster.UpdateHelper`.** The launcher (`ScanMaster.exe`) was
  published as bare self-contained with `TrimMode=full`, which dumped
  ~30 *trimmed* runtime DLLs (`coreclr.dll`, `hostfxr.dll`,
  `System.Private.CoreLib.dll`, …) at the dist root. The .NET host
  inside the separately-bundled `ScanMaster.UpdateHelper.exe` found
  those rogue DLLs in its exe directory and loaded them instead of
  its own bundled (untrimmed) runtime — `TextWriter.WriteLine(object)`
  had been trimmed away, hence the missing-method crash when the
  helper started.

  **Fix:** the launcher is now published as a single-file
  self-extracting bundle (`PublishSingleFile=true` +
  `IncludeAllContentForSelfExtract=true`). Dist root now contains
  only `ScanMaster.exe` and `ScanMaster.UpdateHelper.exe` — no loose
  runtime DLLs to collide with. `Program.cs` switched from
  `AppContext.BaseDirectory` (which points at the temp extract
  folder under single-file) to `Environment.ProcessPath` so the
  launcher still resolves `app\ScanMaster.exe` against the real
  install directory.

  *Upgrade path for affected portable users:* the auto-updater on
  v2.15.22–v2.15.24 portable installs will fail with the missing-
  method error. To get to v2.15.25, either download
  `ScanMasterSetup-2.15.25.exe` (the installer doesn't use the
  helper) or download `ScanMaster-portable-2.15.25.zip` and extract
  over the existing folder. From v2.15.25 onward the auto-updater
  works again.

---

## [2.15.24] - 2026-06-30

### Changed

- **Page sidebar in the main editor migrated to the native Win32
  `SysListView32`** (the same HWND class File Explorer uses, via
  `WindowsFormsHost` + `NativeListView<PageSidebarItem>`). Replaces
  the WPF `ListBox` with a custom thumbnail + label template that
  NVDA could not read reliably — screen readers now announce "Pages,
  list, Page 1, 1 of N" and each arrow-key press reads the new page
  label without yanking the editor around.
- **Page navigation is now on Enter / double-click** (not on
  arrow-key selection-change). This lets the user arrow through the
  list to hear each page label before committing to a jump.
- The thumbnail column in the sidebar template was always rendering
  as empty (`Thumbnail = null`); the migration drops it cleanly.
  Sidebar is now a single-column "Page" list with proper Windows
  column header and Explorer-style selection.

### Added

- **`NativeListView<T>` selection support** so the helper can drive
  navigate-on-arrow-key UIs in addition to the existing
  navigate-on-Enter pattern. New members: `SelectionChanged` event,
  `SelectedIndex { get; set; }` with a suppression flag (mirrors the
  `_suppress*` pattern in `MainWindow`), and `EnsureVisible(index)`.

---

## [2.15.23] - 2026-06-29

### Added

- **Native Win32 ListView in the batch dialogs.** `BatchAudioDialog`
  and `SplitAndConvertDialog` now host the same `SysListView32` HWND
  class File Explorer uses (via `WindowsFormsHost` +
  `NativeListView<T>`), giving Explorer-grade keyboard behaviour,
  real Windows column headers, and a proper screen-reader UIA role.
  `BatchDocumentConvertDialog` already used this pattern in v2.15.22.

- **New AI providers.**
  - **Ollama Cloud** — the hosted Ollama service at
    `https://ollama.com`. Same `/api/chat` + `/api/tags` surface
    as local Ollama but with `Authorization: Bearer <api_key>`.
    Vision-capable. Unlocks the larger turbo models (gpt-oss,
    qwen3-coder, deepseek-v3.1, …) that don't fit on a workstation.
  - **HuggingFace Inference** — OpenAI-compatible chat completions
    at `https://router.huggingface.co/v1/chat/completions`. The
    model field is a HuggingFace repo path
    (`deepseek-ai/DeepSeek-OCR`, `Qwen/Qwen2-VL-7B-Instruct`,
    `stepfun-ai/GOT-OCR2_0`, `meta-llama/Llama-3.2-90B-Vision-Instruct`,
    …). Model picker uses the HF search API filtered to
    vision-capable, Inference-enabled models sorted by popularity.

- **Cloud OCR tab in Preferences.** The cloud OCR API keys
  (Mistral OCR, Mathpix App ID + Key, Datalab, Doctly, Tensorlake)
  were previously hidden inside collapsed expanders on the OCR tab
  and easy to miss. They now have their own dedicated tab.

- **AI Vision OCR engine.** New `LlmVisionOcrEngine` registered as
  dispatcher key `llm-vision` ("AI Vision (uses AI provider)" in
  the OCR engine list). Wraps whichever AI provider is selected on
  the AI tab and calls `CompleteWithImagesAsync` with a fixed
  transcription prompt. Lights up automatically when the selected
  provider supports vision and (if required) has an API key set.
  Combined with the HuggingFace provider above, this unlocks
  DeepSeek-OCR, GOT-OCR 2.0, Qwen2-VL, InternVL, Florence-2, and
  any other vision-capable model on HuggingFace as an OCR engine.

### Fixed

- **Project-wide build break introduced by `UseWindowsForms` in
  v2.15.22.** Enabling WinForms alongside WPF injected
  `System.Windows.Forms` and `System.Drawing` into the project's
  implicit usings, which then collided with WPF types
  (`ComboBox`, `TextBox`, `RadioButton`, `KeyEventArgs`, …) in
  dialogs all over the app. `<Using Remove="System.Windows.Forms"/>`
  + `<Using Remove="System.Drawing"/>` in `ScanMaster.App.csproj`
  strips the global usings; `NativeListView.cs` (the only
  WinForms-touching file) aliases the types explicitly.
- **Leftover `FileList` references** in
  `BatchDocumentConvertDialog.xaml.cs` after the v2.15.22 rename
  to `FileListHost` (Remove_Click + MoveSelection).

---

## [2.15.22] - 2026-06-29

### Changed

- **Batch Document Convert dialog redesigned to match the user's
  reference layout.**
  - Two tabs: **Files** (the main workflow) and **Additional options**
    (less-common toggles).
  - **Output Folder** is now an editable `ComboBox` that remembers
    the last 8 used folders across sessions
    (`prefs.batch_doc_folder_history`).
  - New **Save documents in the same folder where input files are
    located** checkbox — when ticked, the Output Folder + Browse
    grey out and each converted document is written next to its
    source.
  - Tab 2 hosts the existing "Include subfolders" checkbox plus two
    new ones:
    - **Open output folder when finished** (launches Explorer at
      the first folder written to).
    - **Overwrite existing files without asking** (when off,
      colliding outputs get `(1)`, `(2)`, … appended).
  - All three Additional-options checkboxes persist via
    `prefs.batch_doc_*`.

---


### Changed

- **Update dialog rebuilt from scratch with a flat Grid layout.**
  Top-to-bottom: Current version label + read-only TextBox, New
  version label + read-only TextBox, "What's new" release notes,
  radio choice group, OK + Cancel. Replaces the previous TextBlock-
  with-inlines version that was still rendering empty for some
  users. Initial focus lands on the Current version TextBox so NVDA
  immediately announces "Current version, edit, v…" — no longer on
  a radio (would have flipped the safer default).

---


### Fixed

- **Radio buttons did not auto-select on arrow-key navigation.** A
  user could arrow-key from "Text extraction" down to "PaddleOCR" in
  the PDF Import dialog, see focus on PaddleOCR, but pressing Enter
  still ran Text extraction because the previous radio remained
  checked. Native Windows radio groups change selection in lockstep
  with focus; WPF's default does so only sometimes (depending on the
  parent's `KeyboardNavigation.DirectionalNavigation` setting).
  Added an app-wide `RadioButton` style with a `GotKeyboardFocus`
  EventSetter that auto-checks the focused radio. This fixes every
  radio group across the app at once — PDF Import, Save as Audio
  split mode, Page Setup orientation, Update dialog choice, Split
  and Convert mode, every other group inherits the same behaviour.

---


### Fixed

- **Update dialog rendered completely empty in v2.15.17 / v2.15.18.**
  My new layout wrapped the header in a vertical `StackPanel` containing
  a `Grid` with `Width="*"` columns; WPF's measure pass for this
  combination collapsed the entire DockPanel body to zero height,
  leaving the dialog visually blank and screen-reader-empty even though
  the construction code completed without exceptions. Reverted to the
  pre-v2.15.17 single `TextBlock` header layout, with the current and
  new version numbers built as inline `Run`s + `LineBreak`s — NVDA
  reads both, and the body renders normally again.

  **Important:** if you're on v2.15.17 or v2.15.18, install v2.15.19
  manually from the Releases page — your in-app updater works
  (the check call itself is fine), but the dialog body is empty so
  you can't click Update Now.

---


### Changed

- **Update dialog focuses the "Update now" radio button on open**
  instead of the release-notes pane. Screen readers immediately
  announce the user's primary choice alongside the version-pair
  header, so the user can press Enter to accept without tabbing
  past the notes.

---

## [2.15.17] - 2026-06-29

### Changed

- **Update dialog now shows both versions side-by-side.** A new pair
  of labelled fields — *Current version: vX.Y.Z* and *New version:
  vA.B.C* — replaces the single-line header. NVDA reads each value
  separately so users can hear what they're upgrading from and to
  without re-listening to the whole header. Uses
  `GetEntryAssembly()` for the current version (consistent with
  v2.15.16's UpdateChecker fix).

---


### Fixed

- **Updater offered the same version you were already running.**
  `UpdateChecker` was reading `Assembly.GetExecutingAssembly()`, which
  inside ScanMaster.Core resolves to `ScanMaster.Core.dll` — a library
  that has no `<Version>` element, so it always reported 1.0.0.0.
  Compared against the GitHub tag, every release looked newer. Switched
  to `GetEntryAssembly()` so the running app's actual version is used.
- **Update dialog radios were three separate tab stops.** Wrapped them
  in `KeyboardNavigation.TabNavigation="Once"` +
  `DirectionalNavigation="Cycle"` so Tab enters the group once and
  arrow keys cycle between options — the standard WPF radio-group
  pattern.
- **Editor context menu — NVDA skipped Cut / Copy / Paste / Select All
  when nothing was selected.** WPF's auto-disable on `Command` made
  the menu items unfocusable for some screen-reader configurations.
  Replaced the Command binding with Click handlers that probe the
  underlying RoutedCommand; the items stay enabled (so NVDA always
  announces them) and the action silently no-ops when not applicable.
- **Heading-level row in Save-as-Audio / Batch Audio is now hidden
  entirely** when "Single file no chapters" is selected (not just
  disabled). Driven by an XAML binding through
  `InverseBoolToVisibilityConverter`, so no event-handler race exists.
- **Print dialog wasn't showing all standard controls.** Set
  `UserPageRangeEnabled`, `MinPage`/`MaxPage`, and
  `PageRangeSelection` defaults explicitly. The dialog now shows
  page-range and copies controls every time.
- **Menubar still unresponsive after the Print dialog closed.**
  Strengthened `RestoreInputFocus` — clear/reset WPF's focus chain
  with `Keyboard.ClearFocus()` and `FocusManager.SetFocusedElement`,
  and run the whole sequence twice (Input + ContextIdle priorities)
  so the Alt key reliably wakes the menu back up.
- **Batch convert dialogs showed CLR class names instead of file
  names** in some screen readers. Fixed by:
  - Adding `ToString()` overrides to the item types so the default
    accessible name is the file name.
  - Switching the Audio batch list to `DisplayMemberPath="Name"` and
    setting `AutomationProperties.Name` on the row container.
  - Wiring the Document batch list to a Run-based template so the
    `Status` updates re-render correctly and the row's accessible
    name stays the file name.
- **Batch dialogs tab order** now follows the spec: ListView → Add
  files → Add folder → Remove → Remove all → Move up → Move down →
  Recursive → Output folder → Browse → Output format (doc only) →
  Convert → Close. Explicit `TabIndex` on every focusable control.

### Added

- **Page Setup** gained **Gutter** (inside-margin space for binding)
  and **Two-page facing** (mirror inside/outside margins). Persisted
  via `prefs.page_setup_gutter` / `prefs.page_setup_facing`.
- **Page Setup units combo** now reads "Centimeters" / "Inches" in
  full instead of `cm` / `in`.

---


### Fixed

- **Heading-level combo could stay enabled** when "Single file no
  chapters" was selected, despite the v2.15.14 disable logic. Replaced
  the event-handler-driven update with a direct XAML data binding
  (`LevelRow.IsEnabled = !SplitSingle.IsChecked` via a tiny
  InverseBoolConverter), so the combo state is *always* in lockstep
  with the radio — no more race window where the user's click and
  WPF's event ordering could leave the combo enabled.

### Changed

- **Batch Convert to Audio** and **Batch Document Convert** file
  lists are now plain ListView controls (no column headers / grid
  view). Each row shows the filename; the full path is exposed via
  tooltip and as the screen-reader name. (User reported the prior
  GridView columns "looked like a grid, not a proper listview".)

---


### Fixed

- **Supertonic dropped words at rate 0.** Two compounding bugs:
  - The SAPI→speed mapping returned **1.75** at rate 0 instead of
    **1.0**, so the neural model rendered audio at nearly double
    speed and chunks were too short for the MediaPlayer's
    state-machine to catch reliably. Mapping is now piecewise and
    anchored: `rate=0 → 1.0`, `rate=−10 → 0.5`, `rate=+10 → 2.0`.
  - Between chunks the shared MediaPlayer's "Ended" state could leak
    into the next chunk's `Source` assignment, re-raising MediaEnded
    immediately for the new buffer. We now explicitly null the
    Source and reset PlaybackSession.Position between chunks.
- **WinRT engine was also ~2.25× too fast at rate 0.** Same
  fix — piecewise mapping anchored at 1.0.
- **Heading-level combo behaviour.** The user asked for the combo to
  be *disabled* (greyed but visible) when "Single file no chapters"
  is selected; v2.15.12/.13 collapsed the whole row instead. Now it
  stays in place, just disabled and skipped by Tab.

### Changed

- **Batch Document Convert** field order matches the user's spec:
  Output folder + Browse first, then Output format.

---


### Fixed

- **File ▸ Split and Convert crashed the application.** The mode-radio
  `Checked` event fired during XAML construction, before the dependent
  textboxes were created — `UpdateEnablement()` NRE'd and the
  unhandled exception terminated the app. Added a null-guard that
  defers enablement until the visual tree is fully wired.
- **File ▸ Page Setup crashed the application.** Same load-order race
  inside `UnitsCombo_SelectionChanged`. Same guard fix.
- **Auto-updater still returned 404.** The source repo is private; the
  GitHub REST API returns 404 to anonymous HTTP for private repos, so
  the in-app updater literally could not see any release. The updater
  now points at a public mirror repo (`ScanMaster-releases`)
  that holds release tags + assets only.
- **Outline / Contents tree lost focus on arrow keys.** `ScrollToHeading`
  set the editor's `CaretPosition`, which forces focus into the
  RichTextBox. Now only the Enter-key path moves the caret; arrow-key
  browsing keeps focus in the tree.
- **System Print dialog left the menubar unresponsive.** After Print,
  WPF didn't always restore the input chain — Alt-shortcuts and clicks
  on the menubar were ignored until the user clicked the window. We
  now reactivate the main window and refocus the editor on every Print
  exit path.

### Changed

- **Batch dialogs (Audio + Document) added Move up / Move down.**
  Keyboard-driven reordering for multi-select rows.
- **Batch Document Convert always writes `<basename>.<ext>`** — dropped
  the filename-pattern textbox (the previous default value, which is
  also what users wanted).
- **Print Preview** focuses the Print button on open.

---


### Fixed

- **Auto-updater returned 404 / "Could not reach GitHub".** The check hit
  `releases/latest`, which 404s when the most recent release is not flagged
  as "Latest" on GitHub (gh CLI does not always set that flag). The
  checker now pulls a small page of recent releases and picks the first
  non-draft, non-prerelease entry — robust regardless of how the release
  was published.
- **Heading-level combo stayed visible when "Single file, no chapters" was
  selected** in Save as Audio. The whole heading-level row now collapses
  for that mode, and `UpdateEnablement` is also called from `Loaded` to
  catch the load-order race where the radios fire `Checked` before
  `Initialize()` runs.
- **About dialog had no initial focus and the tab order was wrong.** The
  version textbox now gets focus on open; Tab walks Version → Copy →
  Copyright/License → Close.
- **Supertonic engine cut off after the first sentence.** The shared
  `MediaPlayer` is now explicitly paused before assigning each chunk's
  `Source` — without this, `MediaEnded` from the previous chunk leaked
  into the new buffer's first poll and the consumer loop thought
  playback was done.
- **NVDA's "report status bar" went silent after opening a document.**
  Opening a document let the editor's `RichTextBoxAutomationPeer` shadow
  the status bar in NVDA's cached traversal. The status bar peer now
  raises a structure-changed event after every document selection so the
  screen reader re-resolves it.
- **Editor right-click menu was missing Undo and Redo.** Inserted at the
  top of the dynamic context menu so they match every other Windows
  editor.
- **Page Setup opened the system Print dialog instead of a real Page
  Setup dialog.** New dialog with paper size (A4 / Letter / Legal / A5 /
  Custom), orientation (Portrait / Landscape), and four margin inputs
  (cm or in). Values persist globally and are honoured by Print, Print
  Preview, and PDF export.

### Added

- **AI image description progress.** "Describe with AI" now announces
  three phases through the status bar (and therefore NVDA): "Sending
  image for description", "Receiving description", "Image description
  done".
- **Batch convert audio overhaul.** ListView with Filename / Folder /
  Size columns; **Add folder…** with **Include subfolders** recursive
  toggle; **Remove all** to clear the list; the list receives focus on
  open.
- **Batch Document Convert dialog.** The old File ▸ Export As… (a
  duplicate of Save As) is replaced by a real batch tool: pick any
  number of files or whole folders, choose a single output format
  (docx / epub / pdf / html / txt / rtf / md / odt / smdx), and convert
  them all in one pass. Per-file Status column shows Pending →
  Converting → Done / Failed.
- **Split and Convert dialog.** Slice the active document into multiple
  smaller documents by heading level, section break, volume / chapter,
  regular expression, every N pages, or every N words. Preview the
  planned slices before running. Output is documents only — audio
  exports go through Batch Convert to Audio.

---

## [2.15.11] - 2026-06-28

### Fixed

- **Speech rate used two different scales across the app.** The status bar
  and Save-as-Audio dialog showed words-per-minute (200, range 50–400 or
  50–600 depending on site), while `SpeechSettingsDialog`, `SapiTagDialog`,
  and the engines' internal state used SAPI scale (−10..+10). All
  surfaces are now SAPI scale end-to-end: status bar shows `Rate:+3` or
  `Rate:-5`; Preferences slider is −10..+10 with one-step ticks; Save-as-
  Audio Rate field accepts −10..+10. Engines map internally to their
  native ranges (Sapi5 direct, WinRT 0.5–4.0, Supertonic 0.5–3.0). A
  one-time migration on first launch converts any legacy WPM values
  stored in `prefs.speech_rate` (and adopts the value from
  `prefs.speech_sapi_rate` if it was set), then deletes the dead key.

- **Auto-updater always reported "you are on the latest version"** even
  when a newer release existed. Two compounding causes:
  - `Version.Parse("2.15.10")` returns revision = −1, while
    `AssemblyVersion` is `2.15.10.0` (revision = 0). .NET treats −1 as
    *less than* 0, so the equality comparison silently failed. Both
    sides are now passed through `Normalize()` that pads to 4
    components with `Math.Max(component, 0)`.
  - The manual "Check for updates" path returned a misleading "you are
    on the latest version" for *every* null return, including transient
    network failures and stale-ignore states. The checker now returns
    a structured `CheckResult { Status, Info, Error }` and the UI shows
    three distinct messages: Update available → opens the dialog,
    Up-to-date → confirms the version, Check failed → "Could not reach
    GitHub" with the underlying error message.
  - The manual check also clears `update.ignored_version` before
    running, so a previous "Ignore this version" click can't silence an
    explicit user request.

- **Save-as-Audio: initial focus** lands on the Format combo when the
  dialog opens. A new `AudioOptionsPanel.FocusFirst()` method exposes
  the Format combo to the host dialog, and `AudioExportDialog` dispatches
  the focus call at Input priority so it survives WPF's window-
  activation pass (same v2.15.5 pattern as the Help/Dictionary dialogs).

- **Bitrate combo was missing options.** Extended the list to ten values:
  32 / 64 / 96 / 128 / 160 / 192 / 224 / 256 / 320 / 384 kbps.

- **Output-structure radio buttons acted as three independent tab stops.**
  Wrapped them in a `StackPanel` with `KeyboardNavigation.TabNavigation
  ="Once"` and `DirectionalNavigation="Cycle"` — the standard WPF radio-
  group idiom. Tab enters/exits the group once; arrow keys cycle
  between the three options inside.

- **Heading-level combo stayed a tab stop even when disabled.** Tab now
  skips it when "Single file no chapters" is selected (the only mode
  where heading level doesn't apply); enabled and reachable for the
  other two output structures.

### Internal

- `AudioExportOptions.RateWpm` → `Rate` (still `int`, now SAPI scale).
- `RenderVoice.RateWpm` → `Rate`. `AudioExportSupport.SapiRateToWpm`
  deleted along with `MainWindow.WpmToSapiRate` / `SapiRateToWpm`.
- `ISpeechEngine.SetRate(int sapiRate)` — XML doc updated; all engine
  impls drop their WPM-conversion math (SAPI5 just clamps; WinRT and
  Supertonic apply their native maps directly).
- `SpeechManager.SetSapiRate` retained as a one-line forwarder to
  `SetRate` for source compatibility.

---

## [2.15.10] - 2026-06-25

### Fixed

- **Ctrl+PgDn / Ctrl+PgUp stopped navigating pages after the Find/Replace
  dialog's GoTo tab was used.** `NextPageCommand` / `PrevPageCommand` were
  routed through `NavigateBy(_navigationTarget, ±1)`, which got mutated to
  "Heading 1" (or Bookmark / Comment) the moment the user changed the GoTo
  target. Even after closing the dialog the field stayed sticky and page
  navigation silently failed when the document had no matching heading.
  `NextPageCommand` / `PrevPageCommand` now ALWAYS step by page; the
  Browse-By behaviour moved to new `GoToNextTargetCommand` /
  `GoToPrevTargetCommand`, and the dialog resets `_navigationTarget` to
  "Page" on close as belt-and-braces.

- **Speech became sluggish after the first Stop → Start cycle.** The
  three-stage `RobustSpeechStopper` (added in v2.15.0) waits up to 300 ms
  before calling `engine.Reset()`, which disposes and recreates the SAPI5
  synth. If the user clicked Start within that window, the new pipeline
  attached its `BookmarkReached` / `SpeakCompleted` handlers to the
  about-to-be-disposed synth — handlers then leaked across cycles,
  growing the dispatcher queue and making each subsequent cycle slower.
  Two fixes: (1) `_stopTask` captures the in-flight stop and every Speak
  entry point awaits it (500 ms ceiling) via a new `FireAndForgetSpeak`
  helper before building a new pipeline; (2) `Sapi5Engine` gains a
  generation counter bumped by every `Reset()`, and in-flight pipelines
  bail cleanly when they detect their attached synth is no longer the
  active one.

- **"Pause / Resume" appeared twice in the Speech menu.** Once with
  `InputGestureText="F3"` and once with `Ctrl+Space`. Removed the
  duplicate; the F3 gesture is now updated dynamically by
  `SyncMenuShortcuts` to whatever the user has bound for `speech.pause`,
  and the existing top-level Ctrl+Space `KeyBinding` keeps that chord
  functional from the keyboard.

- **NVDA's "report status bar" command (NVDA+End) read nothing useful.**
  `AccessibleStatusBar` exposed a `StatusTextProvider` callback that
  `StatusBarAutomationPeer.GetNameCore` returned as the UIA Name — but
  nothing in `MainWindow` ever set the callback, so the Name was an empty
  string. The composed status line is now wired up
  (Page / Line-Col / Style / Words / Speech / File, joined by em-dashes),
  and a UIA `Name`-property change event fires whenever any of the
  underlying `TextBlock`s is updated so NVDA picks up the latest value
  on every read-status invocation.

- **Audio-export process priority could stick at Idle / High** if anything
  threw before the explicit `finally` block ran (Task.Run scheduling
  failures, dialog-close races, etc.). The whole ScanMaster process
  ended up throttled or aggressive for the rest of the session — making
  speech callbacks and the UI feel frozen. The priority dance now lives
  in a new `ProcessPriorityScope : IDisposable`, and the audio export
  sites use `using var _ = ProcessPriorityScope.Apply(tuning);`. C#'s
  `using` semantics guarantee disposal on every exit path including
  unhandled exceptions. `App.OnExit` also defensively forces priority
  back to Normal so a future launch never inherits a corrupted value.

### Internal

- New `ScanMaster.Core/Audio/ProcessPriorityScope.cs` — IDisposable
  priority restorer + `ForceNormal()` shutdown safety net.
- `StatusBarAutomationPeer.RaiseStatusUpdated()` pushes UIA
  Name-property change events; `AccessibleStatusBar.NotifyStatusChanged()`
  forwards to it. MainWindow attaches a `DependencyPropertyDescriptor`
  value-changed listener to each status TextBlock to call this.
- `Sapi5Engine.Generation` exposed for `RunChunkPipeline` to detect
  stale generations after Reset(); event handlers now snapshot the
  active synth at attach time so they detach from the right one.

---

## [2.15.9] - 2026-06-25

### Fixed

- **Portable automatic updates could fail on systems without a machine-wide
  .NET runtime.** `ScanMaster.UpdateHelper` is now published as a
  self-contained single-file binary, matching the main app's deployment model.
  This prevents helper startup failures during Help > Check for updates in
  portable installs.
- **Speech profile selection was not consistently honored after closing Speech
  Settings.** Confirming Speech Settings now persists the currently selected
  speech profile as active, so per-style speech overrides reliably use the
  profile the user selected.
- **Speech rate behavior was inconsistent across startup/settings paths due to
  mixed preference keys and scales.** Compatibility handling now keeps
  `prefs.speech_sapi_rate` and `prefs.speech_rate` aligned for SAPI usage.
- **Intermittent speech restarts could fail after navigation/restart actions.**
  Restart paths now use immediate stop behavior to avoid delayed reset races
  from asynchronous robust-stop escalation.

### Added

- **Speech preference regression coverage.** Added
  `SpeechPreferencesRegressionTests` to lock profile activation behavior and
  SAPI/WPM speech-rate compatibility.

### Internal

- Bumped product version metadata to **2.15.9** across app project,
  updater-helper project, installer script, and top-level docs/help version
  references.
- Updated build scripts so release and development packaging publish
  `ScanMaster.UpdateHelper` self-contained.

---

## [2.15.8] - 2026-06-24

### Fixed

- **Sensitive local data was stored in plaintext in user settings and clip
  storage.** `PreferencesDb` now encrypts all values in the `settings` table at
  rest using DPAPI (`CurrentUser`) with transparent read/write behavior.
  Existing plaintext rows are auto-migrated to encrypted format on first read.
  `ClipStore` now stores `clips.json` in encrypted form with the same
  auto-migration behavior for legacy plaintext files.
- **OCR debug artifacts wrote readable diagnostic content to disk.**
  `ScannedPdfImporter` now writes encrypted diagnostics (`ocr_debug.log.enc` and
  `debug_page_1.png.enc`) under `UserDataDirectory` instead of plaintext debug
  files.
- **Debug logs could expose document content.** High-verbosity speech logs no
  longer emit raw text previews or literal spoken words. Diagnostic metadata
  (lengths, offsets, errors) is preserved.

### Added

- **Shared encrypted artifact utility.** Added
  `ScanMaster.Core/Net/EncryptedArtifactStore.cs` to centralize encrypted
  text/byte writes and optional legacy-plaintext migration reads for internal
  support artifacts.
- **Security regression tests.** Added tests for encrypted settings persistence,
  clip storage encryption/migration, and encrypted artifact store behavior:
  `PreferencesDbSecurityTests`, `ClipStoreSecurityTests`, and
  `EncryptedArtifactStoreTests`.

### Internal

- Bumped product version metadata to **2.15.8** across app project,
  updater-helper project, and installer script.
- Updated release/plan/help documentation for the 2.15.8 maintenance release.

---

## [2.15.7] - 2026-06-24

### Fixed

- **Save as Audio used multi-GB of RAM and could freeze the machine** on long
  documents. Root cause: `AudioExporter` accumulated every chapter's PCM in a
  `List<float[]>`, then concatenated the whole document into one more
  `List<float>` before the intermediate WAV write. A 10-hour audiobook at
  24 kHz mono float32 is ~3.5 GB of buffers, doubled by `AddRange` growth
  and the final `.ToArray()` copy. The export now **streams each chapter to
  its own temp WAV** as soon as it's synthesised and drops the buffer
  before the next chapter starts. Peak in-memory PCM is bounded by **one
  chapter** (typically &lt; 200 MB) regardless of book length. The single-file
  output path uses ffmpeg's concat demuxer fed the per-chapter WAVs, so the
  encode itself also streams sample-by-sample with constant memory.

### Added

- **Audio export priority picker.** New ComboBox under "Resource use" in
  the Save-as-Audio dialog (and in Batch convert audio) with five levels:
  **Very low / Low / Normal (default) / High / Very high**. The choice
  controls:
  - **Process priority** (`ProcessPriorityClass`) — Idle, BelowNormal,
    Normal, AboveNormal, or High. RealTime is deliberately excluded.
  - **Worker-thread priority** (`Thread.Priority`) on the export task.
  - **ONNX intra-op thread cap** for Supertonic — 1 at Very low,
    cores/2 at Low, ORT default (all cores) at Normal/High/Very high.
    Inter-op is pinned to 1 and execution forced sequential at the
    capped settings (Supertonic chains four sessions in series anyway).
  - **ffmpeg `-threads`** — 1 at Very low, 2 at Low, default otherwise.
  - **Inter-block yield** — 2 ms / 1 ms / 0 below Normal so the OS
    scheduler can hand time to foreground apps.

  Normal preserves pre-v2.15.7 behaviour. The choice is persisted under
  `prefs.audio_priority` and a live hint label describes the trade-off
  for the focused option (announced by NVDA via `LiveSetting="Polite"`).

### Internal

- New `PriorityTuning` record + `Resolve(AudioExportPriority)` helper in
  `AudioExporter.cs` so the five concrete knobs always move together.
- `SupertonicInference.Load` gains an `onnxThreads` overload threaded
  through `AudioRendererFactory.Create(engine, onnxThreads)` →
  `SupertonicRenderer(int)` so live playback (always 0 = ORT default)
  remains unchanged.
- `FfmpegEncoder` accepts an optional thread cap and a new
  `inputIsConcatList` flag for the ffconcat-demuxer single-file path.
- Process / worker-thread priority is restored in a `finally` block in
  both `MainWindow.RunAudioExport` and `BatchAudioDialog`, so a crashed
  or cancelled export can never leave the whole app stuck at Idle / High.

---

## [2.15.6] - 2026-06-24

### Fixed

- **Installer was missing the Supertonic neural TTS models** (~380 MB of
  ONNX models + voice styles). The v2.15.x installers were ~648 MB instead
  of the expected ~1.2 GB. Root cause: `build-release.ps1` wipes
  `dist\ScanMaster\app\` before `dotnet publish` rebuilds it — and the
  Supertonic ONNX models live ONLY in that folder (they're too large to
  commit to the source tree). Every build silently dropped them. The
  installer also had `skipifsourcedoesntexist` flags on those entries from
  an earlier debugging session, so iscc completed without complaint.
  The build script now stashes `speech\supertonic\onnx\` and
  `speech\supertonic\voice_styles\` to `%TEMP%` before the wipe and
  restores them after publish, so a complete installer with all neural
  voices is produced every build.

---

## [2.15.5] - 2026-06-24

### Fixed

- **New v2.15 dialogs didn't focus an input control when they opened.** WPF
  `Window.Show()` leaves keyboard focus on the window itself, so screen-
  reader users heard nothing and sighted users saw no caret or highlight
  until they pressed Tab. The fix that every dialog needs is the same
  three lines: hook the `Loaded` event, dispatch at `Input` priority (so
  the focus survives WPF's window activation pass), call `Focus()` plus
  `Keyboard.Focus()` so logical AND keyboard focus end up on the target.
  Applied to:
  - **Help › Release Notes** — focus lands in the notes pane.
  - **Update available** dialog — focus lands in the release-notes pane
    so the user can read "what's new" before deciding.
  - **Tools › Dictionary** — focus lands in the Word search box (and
    selects any pre-filled word so typing replaces it cleanly).
- **Dictionary tab order rearranged.** Without explicit `TabIndex`, the
  DockPanel layout made Tab jump from the Lookup button straight to the
  Insert/Copy/Close buttons, skipping the results tabs. Tab now walks:
  Word → Lookup → Back → result tabs → Insert → Copy → Close.

### Internal

- New `WindowFocusHelper.FocusOnLoaded(target)` extension — one-line
  pattern any future dialog can use to schedule initial focus correctly.

---

## [2.15.4] - 2026-06-24

### Fixed

- **NVDA read every line twice in the Dictionary Definitions and Examples
  tabs.** Both tabs had `AutomationProperties.Name="Definitions"` /
  `"Example sentences"` on the read-only TextBox AND the TabItem header
  named the same control. NVDA announced each line via both the focused-
  control Name path and the UIA TextPattern caret-move path. The
  AutomationProperties.Name has been removed from both TextBoxes — the
  TabItem header alone is now the screen-reader label, and each line is
  announced exactly once on arrow-down / line navigation.

### Added

- **Describe Image with AI.** New Format > Describe Image with AI… menu
  entry and a right-click context-menu entry (visible only when the caret
  is on an image). Calls the configured AI vision provider (OpenAI GPT-4o,
  Anthropic Claude, Google Gemini, etc. — anything where
  `IAiProvider.SupportsVision == true`), gets a detailed accessibility
  description of the image bytes, and writes that description on three
  layers so subsequent passes read it back:
  1. The WPF paragraph's `ImageAlt` attached property
  2. The transparent in-flow alt run that NVDA reads in natural reading order
  3. The underlying DOM `Block.ImageAlt` so the next save and next document
     reload retain the new alt text.
  Uses the same prompt key (`prefs.ai_image_alt_prompt`) as the OCR
  proofread "describe images" flow so users can tune one prompt for both.
  Feature key `format.describe_image` is registered in Keyboard Manager
  with no default chord (assign one in Tools > Keyboard manager if desired).

---

## [2.15.3] - 2026-06-24

### Fixed

- **Dictionary dialog showed the word but no definitions** when opened with a
  selected word from the editor. Two issues fixed together:
  1. The lookup ran before the WPF window finished its initial layout pass,
     so the RichTextBox sometimes never displayed the FlowDocument that was
     assigned to it. The lookup now runs from the window's `Loaded` event
     and is guaranteed to fire when the controls are real and visible.
  2. The Definitions and Examples tabs now use plain read-only `TextBox`
     controls (with `IsReadOnlyCaretVisible="True"`) instead of `RichTextBox`.
     A regular TextBox renders text more reliably across builds and gives
     screen-reader users a normal caret-driven reading experience
     (character / word / line navigation works the way they expect).
- **Dictionary "No entry" responses were silent.** When WordNet has no match
  for the word, the Definitions tab now shows a brief message ("No entry for
  X — try a different spelling…") instead of leaving the pane blank.

---

## [2.15.2] - 2026-06-24

### Fixed

- **Help › Release Notes froze the application.** The lightweight markdown
  renderer's inline-styling loop deadlocked the moment it hit a stray `*`
  outside a `**bold**` pair: `IndexOfAny(['*', '`'], i)` returned the same
  position `i`, the loop made no progress, and the UI thread spun on a
  hot loop forever. The same bug existed in the auto-update dialog's
  release-notes renderer. Both `AppendInline` helpers now start the
  next-token search at `i + 1` and emit unterminated `**` / `` ` `` runs
  verbatim, guaranteeing strict loop progress.

---

## [2.15.1] - 2026-06-24

### Fixed

- **Dictionary lookup returned "No entry" for many common words** (`computer`,
  `system`, etc.). Root cause: WordNet `index.<pos>` lines end with **two
  trailing spaces** before the newline, and the parser used
  `string.Split(' ')` which produces empty trailing tokens. The
  "last `synset_cnt` tokens are the offsets" arithmetic then picked up empty
  strings instead of the actual offsets, so the bucket for those words
  contained zero synsets and the dialog reported no entry. `WordNetLookup` now
  uses `Split(..., RemoveEmptyEntries)` for both index and data files.

- **Help › Release Notes showed an empty TreeView.** v2.15.0 attempted to parse
  `CHANGELOG.md` into a structured tree of versions/sections/bullets, which
  was fragile across dev / portable / installed paths and silently produced
  no items when the file wasn't found at the right location. The dialog now
  renders the full CHANGELOG.md as a scrollable markdown view in a single
  read-only `RichTextBox` — simpler, robust, and screen-reader friendly with
  the existing `IsReadOnlyCaretVisible` pattern. The Refresh-from-GitHub
  button still works.

- **CHANGELOG.md was not bundled in the portable zip** (it was only copied by
  the installer). The portable build now copies the repo-root CHANGELOG.md to
  `dist\ScanMaster\help\` and the dev `ScanMaster.App.csproj` does the same
  via a `Content Include` so F5 / `dotnet run` finds it at the same path.

---

## [2.15.0] - 2026-06-24

### Fixed

- **Installed-mode SQLite "unable to open database file" crash.** `PreferencesDb`
  pointed at `{install dir}\scan_master.db`, which under an Inno Setup install
  resolves to `C:\Program Files\ScanMaster\` — a UAC-protected folder where
  standard users cannot write. `AppPaths` now exposes `IsPortable` and a new
  `UserDataDirectory`; installed mode redirects the prefs DB, downloaded
  tessdata, OCR debug logs, scanmaster.log, and the release-notes cache to
  `%LocalAppData%\ScanMaster\`. A one-time migration moves a pre-v2.15 DB
  sitting next to the exe into the new location so upgrade users keep their
  settings. The Inno installer creates the folder up front so first launch can
  never hit an EPERM. Portable installs are unchanged.

- **Help TreeView lost the user's place after tabbing into the content pane
  and back.** Focus landed on the first visible TreeViewItem instead of the
  previously selected topic, forcing screen-reader users to re-navigate from
  the top of the tree every time. `HelpDialog` now hooks `TopicTree.GotFocus`
  and re-focuses the selected item.

- **Stop sometimes did not stop speech.** A single `Stop()` call on SAPI / WinRT
  MediaPlayer / Supertonic could race against a buffer already handed off to
  the audio device, so the user heard the rest of the current chunk before
  silence. Added a three-stage `RobustSpeechStopper`: best-effort `Stop()` →
  second `Stop()` 150 ms later → full `Reset()` (dispose+recreate the
  underlying synth / detach the MediaPlayer source / cancel the ONNX session)
  if the engine is still producing audio after 300 ms. Each escalation is
  logged so future bug reports point at the right engine.

### Added

- **Tools › Dictionary…** (`Ctrl+Shift+D`) — full offline dictionary backed by
  the bundled WordNet 3.x database. Shows definitions per part of speech,
  synonyms, antonyms, example sentences, and related (broader / narrower)
  terms for any English word. Defaults to the word at the editor caret;
  double-click or press Enter on a synonym to look it up in-place; **Insert**
  replaces the editor selection with the highlighted word. F1 opens the
  dictionary help topic.

- **Help › Release Notes…** — browses the project's `CHANGELOG.md` inside the
  app. Left-pane `TreeView` lists every version (newest first); expanding a
  version shows Fixed / Added / Internal bullets. The bundled copy ships with
  the installer; a **Refresh from GitHub** button pulls the latest CHANGELOG
  from `main` and caches it under `%LocalAppData%\ScanMaster\cache\`.

- **Help › Check for updates…** + automatic daily check. On startup ScanMaster
  asks `api.github.com` for the latest release (at most once every 24h, never
  blocking startup). When a newer version is found an Update dialog shows the
  release notes with three choices: **Update now**, **Remind me later**,
  **Ignore this version**. *Installed mode* downloads the Inno setup exe and
  launches it with `/SILENT /CLOSEAPPLICATIONS /RESTARTAPPLICATIONS`. *Portable
  mode* downloads the zip and hands off to a new `ScanMaster.UpdateHelper.exe`
  (single-file .NET 8 binary shipped alongside `ScanMaster.exe`) which waits
  for the running app to exit, atomically swaps `app\`, preserves `data\`,
  `tools\dictionaries\`, `tools\paddleocr\models\`, `portable.marker`, and
  any `*.log` files, then re-launches ScanMaster.

### Internal

- New `ScanMaster.UpdateHelper` project — tiny console exe published as
  single-file for the portable-update swap-and-restart flow.
- `AppPaths.WritableTessDataDirectory` mirrors bundled traineddata files via
  Win32 hard links into `%LocalAppData%\ScanMaster\tessdata\` on first access
  in installed mode, so `TesseractOcrEngine` and the Language Pack Manager can
  share a single user-writable tessdata path without duplicating disk usage.
- `ISpeechEngine` gains `IsSpeaking` and `Reset()`; SAPI / WinRT / Supertonic
  implementations track speaking state explicitly and provide a hard
  tear-down path.

---

## [2.14.11] - 2026-06-23

### Fixed

- **WIA scan crashed with "Scan error: COM object that has been
  separated from its underlying RCW cannot be used".** Root cause in
  `Wia2Scanner.TryConnect`: it ran `info.Connect()` on a throwaway STA
  thread for timeout safety, then returned the connected `device` RCW
  to `ScanSync` running on a different STA thread. The throwaway
  thread exited; the RCW became orphaned; the next call (e.g.
  `FindScanItem(device)`, `SetPropById`, `TransferPage`) raised the
  RCW-separated error. `TryConnect` now runs `info.Connect()` inline
  on the caller's STA thread so the RCW survives. Per-Connect timeout
  protection is lost; the outer `RunStaAsync` wrapper still enforces a
  hard ceiling via `options.TimeoutSeconds` so the whole operation
  cannot hang indefinitely.

---

## [2.14.10]
 - 2026-06-23

### Fixed

- **Screen readers did not announce menu shortcuts.** The
  v2.14.9 diagnostic log confirmed my menu-sync code WAS writing the
  correct chord into `MenuItem.InputGestureText` (e.g. `set: _New
  feature=file.new chord=Ctrl+N`). The chord text was rendered visually,
  but NVDA / JAWS / Narrator still announced menu items without the
  shortcut. Root cause: WPF wires `InputGestureText` to the visual menu
  template, but it does **not** automatically propagate runtime changes
  into the UIA `AcceleratorKey` automation property that screen readers
  query. `SyncMenuShortcuts` now calls
  `AutomationProperties.SetAcceleratorKey(item, displayChord)`
  explicitly alongside `InputGestureText`, so the chord is exposed both
  visually and to assistive tech.

---

## [2.14.9]
 - 2026-06-23

### Fixed

- **57 features registered in `FeatureRegistry` were not in
  `BuildFeatureCommandMap`.** Symptom in the log: pressing Alt+F4
  dispatched `file.exit` but `cmd=null`, so the chord did nothing
  (Windows closed the app via its own default Alt+F4 handler, masking
  the bug). Same fault applied to Insert > Hyperlink (Ctrl+K), Format
  language/borders/highlight/text-color/tabs, Pages Copy/Reorder/Set-
  Marker, Scan Only / After / Before / At-Begin / At-End / Recognize /
  Languages, all Speech prev/next char/word/line/sentence/paragraph,
  Speech Rate/Pitch/Volume up/down/reset, Tools > AI Assistant /
  Insert Clip / Manage Clips, Edit > Paste Special / Go to Line / all
  Select-* variants, Insert > Endnote / Equation / Footnote / Header
  and Footer / Manage Bookmarks / Object / Symbol / Table of Contents.
  This release adds all 57 mappings. Pressing any of these shortcuts
  in Keyboard Manager now actually invokes the command, and
  `SyncMenuShortcuts` recognises every menu item bound via a
  `{Binding}` so it can write the chord into `InputGestureText`.

(Format > Headings 1-6 and Normal style remain special-cased through
`ApplyHeadingCommand` with a string parameter, unchanged.)

---

## [2.14.8]
 - 2026-06-23

### Added

- **Spell-check dialect picker.** The Spelling dialog now has a
  **Language** combo box at the top of the buttons column that lists
  every dictionary installed in `tools/dictionaries/` (en-US, en-GB,
  en-ZA, fr-FR, de-DE, etc.). Switching the dialect rebuilds the
  Hunspell checker on the fly, restarts the scan from the document
  start, and persists the chosen language to `prefs.spell_lang` so the
  next session remembers it. Fixes the bug where the checker flagged
  British / South African / French / etc. words as misspelled when only
  en-US was loaded by default.

### Diagnostic

- **Menu-shortcut sync now logs to `scanmaster.log`.** I have been
  unable to reproduce the missing-shortcut-text symptom locally, so
  `SyncMenuShortcuts` now writes one line per menu item to the app log:
  header, mapped feature, chord lookup, applied display string -- plus
  a summary line (total / matched / applied / nullCmd). If the symptom
  recurs, attach the log lines under category `MenuSync` and the next
  fix can be targeted at the actual failure mode instead of guessed.

---

## [2.14.7]
 - 2026-06-23

### Documentation

- **Memory + plan + README + help** brought up to date for the whole
  v2.14 series. The Scanner Diagnostics plan now carries an Outcome
  section enumerating the seven follow-up patches (a11y caret fixes,
  deps.json + transitive dep packaging, RichTextBox refresh, menu
  shortcut SubmenuOpened, etc.) and a lessons-captured pointer to the
  new `v2-14-scanner-diagnostics` memory file. README "Scanning and
  OCR" section now lists Scanner Diagnostics with its discovery model.
- **No code changes vs v2.14.6** - this release re-bakes the v2.14.6
  menu-shortcut fix into freshly stamped binaries.

---

## [2.14.6]
 - 2026-06-23

### Fixed

- **Menu shortcut text still not showing next to items**, despite prior
  attempts in v2.13.4..v2.13.5. Root cause: `SyncMenuShortcuts` ran in
  the constructor / first `Loaded` event, but at that point WPF had not
  yet resolved every `{Binding XxxCommand}` on the menu items, so
  `mi.Command` was `null` for many of them and the chord lookup
  silently skipped them. Added a `SubmenuOpened` handler on every
  top-level menu (`File`, `Edit`, `View`, etc.) that re-runs
  `SyncMenuShortcuts` each time the user opens that menu. By then the
  bindings are resolved, so gestures appear immediately and stay in
  sync with any chord the user changes in Keyboard Manager.

---

## [2.14.5]
 - 2026-06-22

### Fixed

- **Help window: selecting another topic in the TreeView did not refresh
  the RichTextBox.** Re-assigning `RichTextBox.Document` is unreliable
  when the editor is focused: WPF sometimes keeps the prior content
  visible. Replaced the assignment with a clear-and-rebuild pattern -
  the new topic's blocks are detached from the temporary FlowDocument
  and re-parented into the existing mounted document, then the caret is
  reset to `ContentStart` and the view scrolled to home so the new
  topic is visible from the top.

### Added

- **About dialog: app-name-and-version textbox + Copy button.** Shows
  `ScanMaster <version>` in a read-only Consolas TextBox with a
  dedicated **Copy** button next to it, so users can paste the exact
  build identifier into a bug report without having to read it
  character-by-character. The textbox keeps the read-only caret visible
  for screen-reader navigation.

---

## [2.14.4]
 - 2026-06-22

### Fixed

- **mDNS browse failed with 'Could not load assembly Zeroconf'** in
  v2.14.0..v2.14.3 binaries. The bundled `dist/ScanMaster/app/Zeroconf.dll`
  was present, but the accompanying `ScanMaster.deps.json` shipped to
  the installer was stale (left over from v2.13.5, before the Zeroconf
  NuGet was added). The .NET runtime uses `deps.json` to decide which
  assemblies to load, so without `Zeroconf` listed there it refused to
  load the DLL even though it was sitting right next to it. Refreshed
  `deps.json` from the v2.14.4 publish output.

(Code-only change; if you already installed v2.14.0..2.14.3 and don't
want a fresh install, just drop the v2.14.4 `app\ScanMaster.deps.json`
in over your existing one.)

---

## [2.14.3]
 - 2026-06-22

### Fixed

- **Help window: caret still hidden even after v2.14.1's RichTextBox
  swap.** WPF's `RichTextBox` (inherited from `TextBoxBase`) does not
  show a caret in read-only mode unless `IsReadOnlyCaretVisible="True"`
  is explicitly set. The caret is what screen readers track for
  line-by-line navigation, so without it NVDA / JAWS / Narrator still
  could not step through help content. Added the missing property.
- **About dialog: same problem on the MIT licence box.** The licence
  `TextBox` was also read-only with the default `IsReadOnlyCaretVisible
  = false`. Set `IsReadOnlyCaretVisible = true` and `IsTabStop = true`
  so the caret appears on focus and the licence text is navigable.

---

## [2.14.2]
 - 2026-06-22

### Fixed

- **Scanner Diagnostics: log box had no caret for screen readers.** The
  read-only log `TextBox` was hiding its caret by default, so NVDA / JAWS
  could not navigate the diagnostic log line-by-line. Added
  `IsReadOnlyCaretVisible=True` + `IsTabStop=True` so the caret appears
  on focus and standard arrow / NVDA reading keys work.
- **Scanner Diagnostics: Enter on a row now runs the connection test.**
  Previously only double-click triggered the test, which is inaccessible
  for keyboard / screen-reader users. Added a `KeyDown` handler on the
  device grid: pressing Enter on the selected row runs
  `TestConnectionAsync` and reports the result the same way double-click
  does.

---

## [2.14.1]
 - 2026-06-22

### Fixed

- **Help window: no caret meant no screen-reader line navigation.** The
  help content was hosted in a `FlowDocumentScrollViewer`, which has no
  insertion point and no UIA `TextPattern` selection support. NVDA / JAWS
  / Narrator could only read the entire window in one chunk (or use
  object-review mode). Replaced with a read-only `RichTextBox`, which
  carries a caret + full TextPattern, so arrow keys / NVDA reading
  commands move through the content one character / word / line at a
  time as expected.

---

## [2.14.0]
 - 2026-06-21

### Added

- **Tools > Scanner Diagnostics dialog** for actively probing scanners and
  document cameras, with raw capability reporting and a copyable log box.
  Closes the long-standing gap where wireless / network scanners that
  Windows had not auto-paired were invisible to ScanMaster.
- **mDNS / Bonjour discovery** (`EsclMdnsBrowser`) - actively browses
  `_uscan._tcp`, `_uscans._tcp`, `_ipp._tcp`, `_privet._tcp` on the LAN
  using the new `Zeroconf` 3.6 dependency. AirPrint Scan and Mopria
  scanners are found without needing Windows to pair them first.
- **Subnet HTTP sweep** (`EsclSubnetProbe`) - last-resort discovery that
  probes every IPv4 host on each active /24 RFC1918 interface for
  `/eSCL/ScannerCapabilities` on ports 80, 443, 8080, 8443. Works when
  mDNS is blocked by the firewall.
- **Document-camera probe** - enumerates WinRT `VideoCapture` devices
  and lists each one's supported resolutions and frame rates.
- **Persistent saved-scanner list** - new `scanner_devices` table in
  `PreferencesDb` with full CRUD. Discovered eSCL devices saved through
  the diagnostics dialog show up in the regular Scan dialog dropdown
  next time, even without re-running discovery.
- **`ScannerManager.GetDevices(prefs, protocol)` overload** that merges
  saved entries into the existing enumeration result, so the Scan dialog
  picks them up transparently.
- **F1 help topic `scanner_diagnostics`** explaining each probe button
  and the discovery flow.
- **Keyboard Manager feature `tools.scanner_diagnostics`** so users can
  bind a chord to the new dialog.

### Internal

- Extracted the self-signed-cert-tolerant `HttpClientHandler` from
  `EsclScanner` into a shared `EsclHttpFactory` so the new mDNS browser
  and subnet probe reuse the same TLS policy.

---

## [2.13.7]
 — 2026-06-21

### Fixed

- **Go To ▸ Heading 1–6 did nothing for documents that don'''t fit on one
  page.** The previous heading navigation only iterated the currently
  rendered FlowDocument paragraphs, which in single-page mode (and the
  windowed continuous mode) is just the current page. The walker now
  iterates the DOM model (`model.Dom.Pages[*].Blocks`) across every page,
  finds the next page containing a Heading <N>, calls `GoToPage` to
  render it, then defers caret placement until the page-render completes
  so the caret lands on the heading paragraph.
- **Ctrl+PgDn / Ctrl+PgUp now actually move by the selected Go To target**
  (the dispatch was already in place, but heading navigation silently
  reported "no hits" because of the rendered-only walker bug).

---

## [2.13.6] — 2026-06-21

### Added

- **Combined Find / Find-and-Replace / Go-To tabbed dialog (Word-style).**
  `Ctrl+F` opens the dialog on the Find tab, `Ctrl+H` on the Replace tab.
  Switching tabs updates the dialog title and accessible name.
- **Go To tab** with a list of navigation targets: Page, Bookmark, Comment,
  Footnote, Endnote, Heading 1–6, Header, Footer. Picking a target retargets
  the **Next Page / Previous Page** commands (`Ctrl+PgDn` / `Ctrl+PgUp`)
  so they move by that type — e.g. select “Bookmark” and `Ctrl+PgDn` jumps
  to the next bookmark instead of the next page. The status bar shows
  “Browsing by: <type>” after each selection.
- **Go To** also exposes its own Previous / Next / Go To buttons inside the
  dialog. Entering a page number or bookmark name in the value box and
  pressing Enter (or clicking Go To) jumps directly there.

### Notes

- Page / Bookmark / Comment / Heading 1–6 navigation is fully wired.
  Footnote, Endnote, Header, and Footer navigation are listed but report
  “not yet implemented” — the underlying DOM iteration will land in a
  follow-up release.

---

## [2.13.5] — 2026-06-21

### Fixed

- **SAPI tags spoken as text during Read All.** The styled-speech path
  (`SpeakStyledAsync`) bypassed the SAPI-tag detector. `Read All` / `Read
  from Cursor` now route through `SpeakAsync` (which converts SAPI 5 XML
  to SSML) whenever the text contains any `<voice|rate|volume|pitch|
  silence|emph|spell>` tag.
- **Undo/redo did nothing in opened documents.** Programmatic document
  loading (`fd.Blocks.Clear()` + `RenderPageRange`) was populating the
  WPF undo stack with every page load and every scroll extension. The
  three load/extend sites in `DocumentView` now toggle
  `IsUndoEnabled = false` around the mutation, leaving the user's undo
  stack empty until they actually edit.
- **Menu shortcut text still blank for many items.** `SyncMenuShortcuts`
  ran in the constructor before WPF resolved `{Binding NewDocumentCommand}`
  etc., so `mi.Command` was null and no shortcut was attached. It now
  runs after `Loaded`. Additionally it no longer blanks out
  `InputGestureText` from XAML for features with no KM chord.

### Added

- **Speech ▸ SAPI Tags ▸ Find Next / Previous Quoted Text** —
  navigates to and selects the next/previous quoted passage (handles
  ASCII `"…"`, curly `“…”`, French `«…»`, single curly
  `‘…’`). Useful for assigning a per-character voice in
  dialogues. Default chords `Alt+Q` / `Alt+Shift+Q`.

### Pending

- Combined Find / Find-and-Replace / Go-to tabbed dialog (Word-style)
  with selectable navigation type — page, bookmark, comment,
  footnote, endnote, headings 1–6, headers, footers — that retargets
  Next/Previous Page commands. Deferred to a follow-up release.

---

## [2.13.4] — 2026-06-21

### Fixed

- **Word Count** appeared under Edit in Keyboard Manager (was already
  moved out of the Edit menu in v2.13.2). Feature renamed
  `edit.word_count` → `tools.word_count`; now lives under the Tools
  category in Keyboard Manager.
- **Menu shortcut text** stayed stale when shortcuts were customised in
  Keyboard Manager. Every `MenuItem` now has its `InputGestureText`
  refreshed from the active `KeyboardManager` profile after init and
  after each Keyboard Manager save.

### Added

- **Format ▸ Styles submenu is now dynamic** — Apply Style, Normal, and
  Heading 1–6 stay at the top; every custom style defined in the active
  document is auto-listed below the separator on submenu open. Each
  entry's shortcut text reflects the chord assigned in Keyboard Manager.
- **Editor right-click ▸ Styles** already listed every style; now any
  chord assigned via `style.<name>` triggers the same handler from the
  keyboard.
- **Keyboard Manager** now contains a **Styles** category populated
  from the active document's quick styles. Assign any chord to a style
  the same way you assign one to a feature.
- **Help ▸ Keyboard Shortcuts** is fully dynamic — every File / Edit /
  Format / Navigation / Speech / Scan shortcut topic is rebuilt at
  render time from `FeatureRegistry` + the active `KeyboardManager`.
  Customising a chord in Keyboard Manager updates the help text on
  the next open. Unassigned features show as `(unassigned)`.
- **About dialog** now opens a proper window with the full MIT licence
  text (read-only, scrollable, screen-reader friendly) instead of a
  short `MessageBox`. `LICENSE` is shipped next to `ScanMaster.exe`.

---

## [2.13.3] — 2026-06-21

### Fixed

- **NVDA repeats status bar** — `NVDA+End` was reading the composed status
  twice (once as the bar's UIA Name, then again from each child item). The
  composed-Name path is removed; NVDA now reads each child once.
- **SAPI tags rendered as text** — `Speech ▸ SAPI Tags` markers (e.g.
  `<rate speed="5">…</rate>`) were spoken literally because the SAPI 5
  XML was passed to `SpeakSsmlAsync` (which accepts only SSML). SAPI tags
  are now converted to SSML before synthesis.
- **Apply-Style picker shortcut** — `Ctrl+Shift+S` now focuses the toolbar's
  Apply-Styles combo. A new `Format ▸ Styles ▸ Apply Style…` menu entry
  exposes it; the combo itself was never removed.

### Added

- **Format ▸ Styles ▸ Apply Style…** (`Ctrl+Shift+S`) — moves focus to the
  toolbar's style combo and opens its dropdown.
- **Editor context menu ▸ Styles submenu** — right-clicking in the document
  now offers a Styles submenu listing every defined style for one-click apply.
- **Relative / absolute SAPI tag variants** — `Speech ▸ SAPI Tags` and the
  editor context menu now offer **Rate (Absolute)**, **Pitch (Absolute)**, and
  **Volume (Relative)** alongside the existing relative rate/pitch and
  absolute volume tags. New attributes: `absspeed`, `absmiddle`, `relativeLevel`.
- **Keyboard Manager** now lists every menu-driven feature (60+ new entries
  across View, Edit, Insert, Format, Pages, Speech, Scan, Tools). Items that
  shipped without a default chord can now be assigned a shortcut.

---

## [2.13.2] — 2026-06-21

### Changed

- **Word Count** removed from the Edit menu (was a duplicate); now lives only
  under Tools.
- **Format ▸ Styles submenu** — Heading 1–6, Normal, and the Styles… dialog
  are now grouped under Format ▸ Styles instead of being scattered across
  the Format menu.
- **Default keyboard shortcuts updated** for clarity and reach:
  - Headings 1–6: `Ctrl+Alt+1` … `Ctrl+Alt+6` (was `Ctrl+1` … `Ctrl+6`)
  - Normal style: `Ctrl+Alt+0` (was `Ctrl+0`)
  - Save As: `F12` (was `Ctrl+Shift+S`)
  - Next / Previous page: `Ctrl+PgDn` / `Ctrl+PgUp` (was `Alt+PgDn` / `Alt+PgUp`)
  - First / Last page: `Alt+PgUp` / `Alt+PgDn` (was `Ctrl+Home` / `Ctrl+End`)
  - Read from cursor: `F2` (was `F5`)
  - Read all (from beginning): `Ctrl+F2` (was `Ctrl+F5`)
  - Pause / Resume speech: `F3` (was `Ctrl+Pause`)
  - Stop speech: `F4` (was `Escape`; `Escape` still works as a secondary)
- The bookmark shortcut `Ctrl+F2` was removed because the chord is now Read All;
  bookmarks remain reachable via the Insert menu (remap in Keyboard Manager if
  you want a new chord).

### Fixed

- **Installer always shows the Destination Folder page**, even when a previous
  install is detected. `UsePreviousAppDir=yes` combined with Inno Setup's default
  `DisableDirPage=auto` had been silently skipping the folder page so users had
  no chance to redirect the install.
- **Installer page order**: Installation Mode (system vs portable) now appears
  *before* the folder page, and the folder page suggests an appropriate default
  per mode (Program Files for system installs; the user's Documents folder for
  portable, which is easy to retarget to a USB drive).

---

## [2.13.1] — 2026-06-21

### Fixed

- **Huge EPUBs no longer freeze the UI** — opening a 700-page / 150 000-block
  dictionary EPUB previously froze ScanMaster for tens of seconds on first
  scroll. WPF's `FlowDocument` becomes slow once it holds more than a few
  thousand blocks. ScanMaster now auto-switches to single-page mode for any
  document with more than 200 pages or 5 000 total blocks; each page renders
  independently into an empty editor and stays fast. Use View ▸ Continuous to
  override the auto-downgrade.
- **EPUB spine items split into sub-pages** — a single XHTML spine item with
  thousands of `<p>` elements (typical for dictionaries) used to become one DOM
  page with all those blocks. The EPUB importer now splits any spine item over
  200 blocks into multiple sub-pages, keeping per-page render cost bounded.
- **Plain-text dictionary files load faster** — `PlainTextImporter` now stream
  reads instead of slurping the whole file with `File.ReadAllLines`, and
  auto-boosts the lines-per-page from 50 to 200 for files over 10 000 lines so
  dictionary-style word lists produce far fewer DOM pages.

### Added

- **Async outline panel** — the Navigation panel's heading scan now runs on a
  background thread with a "Calculating…" placeholder, with cancellation when
  the user switches documents. Opening a huge doc no longer blocks on outline
  generation.
- **Async word count** — Tools ▸ Word Count now runs the count off the UI
  thread and shows a status-bar indicator while it works.
- **Import & render diagnostic logging** — `EpubImporter`, `HtmlImporter`,
  `PlainTextImporter`, and the continuous-view renderer log per-step block
  counts and timings so future perf regressions are easy to triage.
- **Eager log flush** — `AppLogger` now flushes after every line so a UI-thread
  freeze never strands the most recent diagnostic entries in the writer's
  buffer.

---

## [2.13.0] — 2026-06-20

### Added

- **Built-in help system** — comprehensive WPF help viewer with 53 topics across 13
  categories, accessible TreeView navigation, full-text search with match counting,
  and FlowDocument content display. All help content is built into the application —
  no external browser or internet connection required.
- **Context-sensitive F1** — press F1 in any of the 27+ dialogs to jump directly to
  the relevant help topic. Each dialog is wired via `HelpDialog.BindF1()` with a
  `RelayHelpCommand` that opens or navigates the singleton help window.
- **Help menu integration** — Help, Quick Start Guide, and Keyboard Shortcuts menu
  items now open the built-in help viewer instead of launching a browser.

### Fixed

- **Voice selection with hacked OneCore voices** — self-contained publish now correctly
  places the RID-specific System.Speech.dll (1.4 MB) in the app directory instead of
  the 308 KB platform-agnostic stub. The stub did not properly bridge `SelectVoice`
  to the COM `ISpVoice` token for OneCore voices registered under SAPI5 via registry
  hacks. Voices like Microsoft Clara Online and Microsoft Natasha Online now work.
- **Supertonic not appearing in speech profiles** — ONNX model files and voice styles
  were not being copied to the correct `app\speech\supertonic\` directory during the
  build-release process. Fixed by using the proper `build-release.ps1` workflow which
  publishes to the `app\` subdirectory.
- **Stale dist folder cleanup** — removed 37 orphaned DLLs and 4 stale directories
  from the distribution root left over from previous ad-hoc publishes.
- **PDF import dialog** — improved AI post-processing progress reporting with per-page
  status updates and deadlock prevention via `InvokeAsync`.

---

## [2.12.2] — 2026-06-18

### Fixed

- **PDF import regression** — v2.12.1 broke PDF imports by passing a generic "ocr" method 
  instead of the specific engine key. Fixed by wiring `OcrEngine` through `ImportOptions` and 
  using it in `BuildOcrEngine()`. Cloud OCR engines now work in PDF import. Added optional 
  `PreferencesDb` to `ImportOptions` for cloud-engine credential access.
- **PDF import dialog crash** — Added defensive null checks in `PdfImportDialog` constructor 
  and helper methods to ensure the dialog can initialize even if XAML controls fail to load. 
  Prevents `NullReferenceException` when dialog is opened.
- **AI checkbox visibility in PDF import** — Moved the three AI checkboxes (Proofread, Preserve 
  Layout, Describe Images) out of the collapsed OCR engine panel into their own always-visible 
  section. Checkboxes are now shown in all PDF import dialogs.
- **OCR engine panel visibility with Auto method** — When "Automatic" import method is selected, 
  the OCR engine panel is now shown (since the app may decide to use OCR at runtime). Previously 
  it was only shown when OCR was explicitly selected.

---

## [2.12.1] — 2026-06-18

### Added — completion of the v2.12 plan

- **Markdown → DOM round-trip.** When the proofreader (or a Markdown-emitting cloud OCR
  engine) returns Markdown, `InsertScannedPage` now routes through `MarkdownImporter`
  so headings, lists, tables, and emphasis become real DOM blocks instead of one
  paragraph per line. `MarkdownImporter.ParseToBlocks(md)` is the new shared helper.
- **Image alt-text on scanned pages.** AI-generated descriptions are attached to the
  inserted page's new `Page.ImageAlt` field, which round-trips through SMDX via the
  `image-alt` attribute. NVDA reads it on the image panel via `AutomationProperties.Name`.
- **Cloud OCR engines fully wired**:
  - **Datalab Marker** — multipart submit + poll loop against `/api/v1/marker`, returns
    Markdown.
  - **Doctly.ai** — multipart submit + poll loop against `/api/v1/documents/`, handles
    inline `markdown`, `output.markdown`, and `download_url` response shapes.
  - **Tensorlake** — multipart submit; supports synchronous responses and the
    `/documents/{id}` job-status poll fallback.
  - A shared `CloudOcrJob` helper centralises multipart + polling.
- **Vision-not-supported warning** — Preferences ▸ AI shows an inline note when
  *Describe embedded images* is on, telling the user whether the active provider
  supports vision and (when it does) reminding them to pick a vision-capable model.

### Notes

- The three new cloud engine wire formats are best-effort approximations of public
  docs. They are explicitly marked in code with a "verify against current docs"
  comment; each provider may need a small body-shape tweak once tested live.

---

## [2.12.0] — 2026-06-18

### Added — AI-assisted OCR proofreading (multi-provider)

- **Six LLM providers** abstracted behind a new `IAiProvider` interface and registered
  in `AiProviderRegistry`: OpenAI, Anthropic Claude, Google Gemini, Mistral AI,
  OpenRouter, and local Ollama. Each provider implements model-list discovery and
  chat completion with provider-specific wire formats (OpenAI shape, Anthropic
  Messages, Gemini `generateContent`, Ollama `/api/chat`). All six can also
  carry image inputs for vision-capable models.
- **Preferences ▸ AI tab overhaul.** Provider dropdown grew to all six entries.
  The Model field is now an editable ComboBox with a **Refresh models** button
  that calls the active provider's `ListModelsAsync` and populates the list with
  what your API key actually unlocks. API keys are stored per provider
  (`prefs.ai_api_key_<provider>`) so switching providers preserves each one.
  Three new defaults — "Run AI proofread after OCR by default", "Preserve exact
  layout when proofreading", "Describe embedded images" — and an Advanced
  expander with custom prompt overrides.
- **Three post-OCR checkboxes on Scan and Camera dialogs**, each independent:
  - **Proofread with AI** — fix OCR errors (letter swaps, joined/split words,
    broken hyphenation across lines).
  - **Preserve exact layout** — keep headings, lists, tables, indentation,
    columns intact (uses the OCR engine's Markdown when available).
  - **Describe embedded images** — generate accessible alt-text for figures
    via a vision-capable LLM.
- **Camera Capture dialog now does OCR.** New "OCR captured image" checkbox
  feeds the captured frame through the configured OCR engine, then optionally
  through the AI pipeline. When OCR text is produced it is inserted as text
  paragraphs; with Describe-images on and OCR off, the image is inserted with
  an AI-generated alt-text on the `BlockUIContainer`.
- **Cloud OCR engines** added to the OCR engine list (Scan dialog, Preferences):
  - **Mistral OCR** (`mistral-ocr-latest`) — fully wired, returns Markdown.
  - **Mathpix** — fully wired, great for math/LaTeX.
  - **Datalab Marker / Doctly.ai / Tensorlake** — credential fields and engine
    entries are in place; per-engine HTTP bodies will be filled in once each
    integration's request shape is pinned. The engine reports `Available=true`
    once credentials are entered, and a clear "not yet wired" error surfaces
    if invoked. This is the scaffold for a follow-up release.
- **AiAssistantDialog migrated** to the new provider layer. Its old hardcoded
  OpenAI endpoint and model are gone; the dialog now resolves provider, model,
  and credentials from Preferences ▸ AI, so it works with all six providers and
  inherits the same Refresh-models flow.

### Graceful degradation

- All AI calls catch and log exceptions instead of throwing into the OCR loop.
  When the proofread call fails (network, bad key, wrong model), the raw OCR
  text is inserted unchanged.

---

## [2.11.8] — 2026-06-16

### Fixed — responsiveness and broken speech profiles

- **App no longer sluggish.** WPF native spell-check (`SpellCheck.IsEnabled`) was being
  enabled on every editor for documents up to 600,000 characters, and re-applied on every
  page load and Preferences save. The threshold is now 50,000 chars and the re-apply skips
  no-op assignments to `SpellCheck.IsEnabled` / `Document.Language` so layout doesn't churn.
  `prefs.spell_as_you_type` now defaults to **off** — turn it on from Preferences ▸ Spelling
  when you want squiggles.
- **Per-style speech profiles work again.** `BuildParagraph` was storing the raw DOM
  `Block.Style` (always `"Normal"` for headings) into the paragraph's `StyleNameProperty`,
  so a profile entry for `"Heading 1"` never matched. Now stores the synthesised
  `"Heading N"` for heading blocks; `ExtractParagraph` strips it on save so the DOM
  round-trip is unchanged.
- **WinRT + Supertonic neural engines now honour per-style profiles too.**
  `SpeakStyledAsync` was a stub on both engines, so per-style voice/rate only fired on
  SAPI5. Both now split text at block boundaries and apply each block's voice/rate before
  speaking. (Word-boundary highlight offsets are local to each segment.)
- **Spell-check dictionary resolution.** When `prefs.spell_lang` is the bare base subtag
  (e.g. `en`), the resolver now picks any installed regional folder (`en-GB`, `en-US`,
  etc.). Also tolerates the LibreOffice mix where the folder is `en-GB/` but the files
  inside are `en_GB.aff`/`en_GB.dic` — tries both stem forms and any `*.aff`/`*.dic` pair.
- **Removed v2.11.5's invisible per-paragraph style-label run.** Every paragraph carried
  an extra transparent FontSize=1 `Run` to lead-in the role for NVDA; this roughly doubled
  the inline count and compounded the spell-check cost. The AutomationPeer heading level
  and the existing style-at-caret live region already announce style/role.

### Improved — accessible Spell Check dialog

- The Misspelled-word and new **Context** boxes have `IsReadOnlyCaretVisible="True"` so
  arrow keys move the caret and screen readers narrate character / word / line.
- Initial focus is on the misspelled word (was the suggestion list), so the user can
  immediately arrow-read it before deciding.
- New **Context** box shows the full paragraph the misspelled word lives in.
- New buttons that use the configured speech engine **in addition** to the screen reader:
  - **Pronounce** — speaks the misspelled word.
  - **Spell out** — speaks it letter by letter.
  - **Speak context** — speaks the whole context paragraph.

---

## [2.11.7] — 2026-06-15

### Added — Word/LibreOffice-style proofing (offline)

- **Spell-as-you-type squiggle.** WPF's native UIA spelling-error annotation is now enabled per
  editor (`SpellCheck.IsEnabled` + `Document.Language`), so misspelled words show the red squiggle
  and NVDA reads them as "misspelled" via UIA Annotation 60003. Off for documents over 600,000
  characters to keep continuous view responsive. Gated by **Preferences ▸ Spell as you type**
  (now default-on).
- **Context-menu suggestions with offline meanings.** Right-click or Apps-key on a misspelled
  word shows the native `GetSpellingError` suggestions, each annotated "word — meaning" from a
  bundled WordNet 3.1 database. `AutomationProperties.Name` is "word, meaning" so NVDA reads
  both. Includes **Ignore All** (`EditingCommands.IgnoreSpellingError`) and **Add to
  Dictionary** (writes through `SpellChecker.AddWord`).
- **Bundled LanguageTool grammar engine.** Tools ▸ Grammar Check now launches the same engine
  LibreOffice uses, served locally by a bundled Temurin 17 JRE — no internet required. The
  Grammar dialog focuses each issue in the document (live region announces status), and the
  server is reused across calls and killed on app exit.
- **Per-paragraph offset map.** `DocumentTextMap` is the single routine that both extracts the
  plain text sent to LanguageTool and maps issue offsets back to selectable ranges, skipping
  the invisible image-label runs so they never shift offsets. Applying a fix mutates the mapped
  `TextRange` (preserving formatting) instead of replacing the whole document.

### Fixed

- **Spell Check dialog showed nothing.** `SpellChecker` hardcoded `en_US` and resolved dictionaries
  from `AppContext.BaseDirectory`, which is the `app\` subfolder in the portable dist — so it
  always reported "not available". Now reads `prefs.spell_lang` and resolves under
  `AppPaths.HomeDirectory\tools\dictionaries`, trying hyphen / underscore / base-subtag folder
  names. The dialog now focuses the suggestion list (or the unknown-word box) after each
  misspelling so NVDA reads it.
- **Grammar dialog couldn't move focus to issues.** Selecting an issue now selects the matching
  range in the editor and brings it into view.

### Tooling

- New `tools-src\fetch-tools.ps1` downloads the Hunspell dictionaries (17 locales), WordNet 3.1,
  LanguageTool stable, and Temurin 17 JRE into `tools\` (gitignored). `build-release.ps1` mirrors
  the new `dictionaries`, `wordnet`, `languagetool`, and `jre` folders into the dist. Debug F5
  copies `dictionaries` and `wordnet` into the output `tools\` so proofing works without running
  the release script.

---

## [2.11.6] — 2026-06-15

### Fixed

- **Page-navigation crash with images.** Navigating pages (Alt+PageDown) on a page containing an
  image threw `InvalidOperationException` in WPF's undo serialization (`XamlWriter`). The custom
  image type is now public and the image block's metadata is stored as serializable attached
  properties instead of stashing the DOM block (with its generic `List<Run>`) in `Tag`. Verified by
  serializing the document directly.
- **Continuous view never actually activated.** The View ▸ Continuous menu defaulted to checked but
  the view defaulted to paged, and nothing synced them, so books always opened paged and the first
  toggle did nothing. The view now defaults to continuous and syncs to the menu when a document opens.
- **Headings announced twice in continuous view.** Empty navigable paragraphs at page boundaries (a
  gray separator paragraph and form-feed page-break paragraphs) made the screen reader's UIA line
  walk overrun into the next line, so the following heading was read twice. Page boundaries now use a
  top border on the page's first paragraph; form-feed page breaks and empty/whitespace-only
  paragraphs are skipped in continuous view. Verified at the UIA line level (the heading now
  enumerates once).

### Added

- **Line and column indicator** in the status bar, updated as the caret moves (and included in the
  NVDA+End status read). The column counts visible characters, excluding the invisible screen-reader
  style labels.
- **Version number and copyright** in Help ▸ About (e.g. "Version 2.11.6", "Copyright © 2026
  Deenadayalan Moodley. All rights reserved.").

---

## [2.11.5] — 2026-06-15

### Fixed

- **Images now actually speak their description in NVDA** (2.11.4's approach was verified against a
  live NVDA debug log and did *not* work). Two real WPF limitations were found and fixed:
  1. Embedded `UIElement`s in an editable RichTextBox are coerced to UIA `IsEnabled = false`, so NVDA
     announced the picture as "graphic, unavailable" and dropped its name. A custom image automation
     peer now forces `IsEnabled = true`.
  2. WPF's RichTextBox text provider does not resolve an inline embedded object's accessible name back
     to the screen reader (range navigation returns the document and cached property reads fail), so
     NVDA only ever heard the role "graphic". The alt text is now also placed as an invisible
     (transparent) in-flow run that NVDA reads in order — so arrowing onto an image speaks
     "graphic, <description>" with no visible caption. Unlabelled images still announce as "image".

- **Paragraph style/heading is now spoken BEFORE the line text** (true Word order, e.g. "heading
  level 2, Section Two"). 2.11.4 tried to do this with a status-bar live region fired on Up/Down, but
  live-region announcements are always drained *after* NVDA reads the new caret line, so the style
  kept trailing the text. Headings and named paragraph styles now carry an invisible leading label
  that NVDA reads first; plain "Normal" body text is no longer announced at all (matching Word). The
  on-screen status-bar style indicator is unchanged and still reported by NVDA+End on demand.

### Notes

- The invisible screen-reader labels are excluded from save/round-trip, from Find/Replace, and from
  copied plain text. (Copied *rich* text / RTF may still include the label text.)
- Verified end-to-end against a live NVDA debug log, not just WPF's editor-side text.

---

## [2.11.4] — 2026-06-15

### Fixed

- **Screen readers now announce images the way Microsoft Word does.** Images are rendered as inline
  UIA embedded objects (`ControlType.Image` with the alt text as the accessible name) — the exact
  mechanism Word uses and that NVDA/Narrator/JAWS query via the text provider's `GetChildren`. There
  is no visible caption; unlabelled images announce as "image". Confirmed at the UIA layer (the data
  the screen reader actually consumes), not just WPF's editor-side text. Earlier attempts placed the
  image alone on a silent line with a separate visible caption, which screen readers did not reach.

### Changed

- **Paragraph style/heading is announced before the line text on Up/Down navigation** (Word order:
  "heading level 1" then the text). The style is now spoken as the caret leaves toward the
  destination paragraph, ahead of the screen reader's reading of the new line, instead of trailing
  it via the status-bar live region.

---

## [2.11.3] — 2026-06-15

### Fixed

- **Images in EPUB (and HTML) books were dropped on import.** The HTML/EPUB importer ignored `<img>`
  tags entirely, so images never reached the document — a screen reader had nothing to announce. The
  importer now turns `<img>` into image blocks (with alt text), including images wrapped in paragraphs
  and figures. The EPUB importer extracts embedded image bytes into the document's image store and
  resolves each `<img src>` to them, so images display and their captions are announced (see 2.11.2).

---

## [2.11.2] — 2026-06-15

### Fixed

- **Screen readers did not announce images.** Images displayed for sighted users but a bare WPF image
  is not surfaced through the RichTextBox text that NVDA/Narrator/JAWS read, so a blind user could not
  tell an image was present. Image blocks now render the picture together with a visible text caption
  ("Image: &lt;description&gt;", or "Image" when there is no alt text), which is real text in the
  document flow and is therefore announced during normal reading. Applied to the paged view, the
  continuous view, and Insert ▸ Image; image blocks still round-trip verbatim on save.

---

## [2.11.1] — 2026-06-14

### Fixed

- **Images in a document did not show up in the editor.** Image blocks were rendered as empty
  placeholders because the editor never set the image source and the document's embedded image data
  was never passed to it. The editor now resolves each image block's bytes from the document's image
  store (falling back to a file path) and displays it, in both paged and continuous views, with the
  alt text exposed to screen readers.
- **Images were dropped when saving the edited page.** The FlowDocument→DOM extraction ignored image
  containers, so an image on the current page vanished on save. Image blocks now round-trip verbatim.
- **Inserted images did not persist.** Insert ▸ Image now stores the picked image in the document's
  image store under a stable key and inserts it at the caret, so it survives save/reload and round-trips
  through the DOM.

---

## [2.11.0] — 2026-06-14

### Added

- **Save book as audio.** A new **Speech ▸ Save as Audio…** dialog exports the current document to
  MP3, M4A, M4B, FLAC, WAV, or OGG. Output can be split into separate files by a chosen heading level,
  written as a single file with embedded chapter markers (one per heading — verified for M4B/M4A/MP3),
  or a single continuous file. Voices come from either the active per-style speech profile or a single
  engine/voice/rate chosen in the dialog. All three engines (SAPI 5, WinRT, Supertonic) render offline.
- **Batch convert to audio.** **Speech ▸ Batch Convert to Audio…** queues a list of books (any
  importable format — SMDX, DOCX, EPUB, PDF, HTML, TXT, RTF, MD, ODT, DOC, CHM), applies one set of
  audio settings to all of them, and shows per-file progress. Cancellable.
- **Bundled ffmpeg.** Audio encoding and chapter-marker muxing use ffmpeg. Fetch it with
  `scripts/download-ffmpeg.ps1` into `tools/ffmpeg/`; the release build copies it alongside the app.
  WAV export works without ffmpeg.

### Fixed

- **NVDA could not read the status bar with "report status bar" (NVDA+End).** NVDA hit-tests the
  foreground window's bottom-left pixel and walks up for a status-bar role; that pixel fell inside the
  window's invisible resize border, so it never reached the bar. The main window now reports its client
  area as its UI Automation bounding rectangle (no visual change), so NVDA+End reads the status bar. The
  composed status text now also includes the speech state.

---

## [2.10.1] — 2026-06-13

### Fixed

- **Bundled help was stale in published builds.** The csproj copied the help files from an
  obsolete worktree path (`..\..\..\..\..\help`) that no longer exists since the project moved to
  the repo root, so the in-app Help still showed the old Python/wxPython text. Corrected the path to
  `..\help`, so the current help ships with the app.

### Changed

- **Rewrote the help as simple, task-based, step-by-step guides** (Getting Started, Writing and
  Formatting, Scanning and OCR, Working with Pages, Reading Aloud and Moving Around). Plain language,
  keyboard-first, with the AutoCorrect manager and per-style speech profiles documented.

---

## [2.10.0] — 2026-06-13

### Added

- **AutoCorrect management dialog.** A new accessible "Manage AutoCorrect" dialog (rule list +
  Replace/With fields + Add/Update/Delete) replaces the old read-only message box. Reachable from
  Tools ▸ Autocorrect, a "Manage entries…" button on Preferences ▸ Autocorrect, and the editor's
  context menu. Edits apply to the running editor immediately.
- **Editor context menu** (right-click and Shift+F10 / Apps key): Cut, Copy, Paste, Select All,
  "Add selection to AutoCorrect…", "AutoCorrect Options…", and the SAPI Tags submenu.
- **Speech profiles per style.** The Speech Settings ▸ Document Elements list now auto-populates from
  the active document's styles (built-in and custom), so a speech profile can be created for each
  style. Falls back to the built-in element list when no document is open.

### Fixed

- The Preferences ▸ Autocorrect "Enable autocorrect" checkbox had no effect: the runtime read
  `prefs.autocorrect` while Preferences wrote `prefs.autocorrect_enabled`. Aligned to
  `prefs.autocorrect_enabled`.

### Changed

- Help files updated from the original Python/wxPython descriptions to the current C# .NET 8 WPF app
  (native `.smdx` format, `scan_master.db`, WPF FlowDocument / UIA Text Pattern 2.0, .NET regex,
  Tesseract/Windows OCR/PaddleOCR, correct import/export lists).

---

## [2.9.1] — 2026-06-13

### Security

- Pinned authoritative SHA-256 hashes for the four Supertonic ONNX model binaries
  (`duration_predictor`, `text_encoder`, `vector_estimator`, `vocoder`), sourced
  from the Hugging Face LFS oids. Downloads of these files are now hard-verified
  against the pinned hashes and rejected on mismatch.

### Fixed

- `scripts/pin-supertonic-hashes.ps1` query URL: the `?recursive=true` suffix was
  parsed as part of the `$Ref` variable; concatenated it explicitly so the script
  runs.

---

## [2.9.0] — 2026-06-13

### Added

- **Notes pane.** Footnotes and endnotes are now displayed in a read-only,
  screen-reader-navigable "Notes" pane below the editor (numbered per kind),
  completing the in-app footnote experience. The pane refreshes on page change
  and when a note is inserted, and hides when the document has no notes.

### Changed

- Download integrity: added `scripts/pin-supertonic-hashes.ps1`, a maintainer
  helper that reads the authoritative SHA-256 (LFS oid) for the Supertonic model
  files from the Hugging Face API — without downloading them — and emits the
  `ExpectedSha256` block to paste into `SupertonicModelDownloader`. This makes
  hard hash-pinning a one-command step.

---

## [2.8.1] — 2026-06-13

### Fixed

- **Startup crash in the Styles pane.** `FilterCombo`'s initial `IsSelected="True"`
  raised `SelectionChanged` during XAML load — before `StyleList` existed — so
  `StylesPane.Refresh` dereferenced a null control and threw `NullReferenceException`,
  aborting application startup. `Refresh` now no-ops until the pane is fully built.

---

## [2.8.0] — 2026-06-13

### Added — Real footnotes, equations, language preferences

- **Footnotes and endnotes are now real document objects.** A `Note` model
  (`Document.Notes` + `Run.NoteRef`) replaces the previous placeholder that inserted
  literal `[Footnote: …]` text. In-text markers render as accessible superscript
  references (screen readers announce "Footnote N: …"), notes round-trip through the
  `.smdx` format, and they export as native OOXML footnotes/endnotes in DOCX.
- **Insert ▸ Equation** inserts a real plain-text / LaTeX expression (screen-reader
  friendly and round-tripped) instead of silently reusing the symbol picker.
- **Preferences ▸ Languages** is now functional: default document language and default
  writing direction, both persisted and applied to new documents.

### Security

- eSCL: untrusted (self-signed) TLS certificates are accepted only for private /
  link-local / `.local` hosts; TLS 1.0/1.1 dropped in favour of TLS 1.2+.
- Downloaded models and OCR language packs are integrity-checked (pinned SHA-256 when
  available, server-advertised LFS hash otherwise) and truncation is rejected.
- CHM import guards against Zip-Slip path traversal.
- Document hyperlinks open only `http`/`https`/`mailto` directly; other schemes prompt
  for confirmation.
- Pandoc subprocess invocations use `ArgumentList` (robust argument quoting).

### Accessibility

- Field labels / UIA names added to the AI Assistant, Grammar, Comments, Clips, Camera,
  Insert Object, Styles, Borders & Shading, OCR Language Manager, and Input dialogs.
- The Symbol picker grid is keyboard-navigable (arrow keys + Enter).
- Page sidebar thumbnails have accessible names.

---

## [2.4.0] — 2026-05-25

### Added — EPUB DOM Import, Word-Cursor Tracking, Speech Follows Focus, Empty-Tab Replacement

**EPUB → DOM import pipeline (Bugs fixed)**
- `_import_epub()` completely rewritten: XHTML blocks now map to a proper `Document > Page > Block > Run` DOM instead of hard-coded RTF font sizes
- Heading levels `<h1>`–`<h6>` correctly mapped to named styles `"Heading 1"`–`"Heading 6"` so the speech engine honours element speech styles (voice, rate, pitch) per heading level
- `<img>` elements now parsed in `_walk_xhtml_el()` and stored as `Block(block_type="image")` DOM nodes
- Image path resolution fixed: paths are now resolved relative to the containing XHTML file's directory (not the OPF base directory), fixing broken image references in most EPUBs
- All images on a page are now extracted (previously stopped after first image)
- Images embedded directly in RTF output via `{\pict\pngblip …}` / `{\pict\jpegblip …}` blocks so they appear inline in the editor body
- First image on each page also used as the ImagePanel thumbnail in IMAGE / BOTH view modes
- RTF corruption fix in `_blocks_to_rtf()`: double-brace `}}` in f-strings produced stray `}` in RTF output for heading and quote blocks
- `Document.image_data: dict[str, bytes]` field added to DOM dataclass; threaded through `page_to_rtf()` → `_block_to_rtf()` so image data is available at render time
- `_get_rtf_for_page()` in `document_view.py` passes `doc.dom.image_data` to `page_to_rtf()` — editor always renders from DOM when a DOM is attached

**Speech word-cursor tracking**
- `_build_block_ssml()` now accepts `base_editor_offset` and `word_tracking` parameters; when `word_tracking=True` injects `<mark name="wb_{offset}_{len}"/>` before every word in SSML
- `speak_page_from_dom()` computes running block offsets from `editor_text` and enables word marks when `on_word_boundary` is wired
- `speak_all()` and `speak_page()` pass `editor.GetValue()` as `editor_text` on the DOM code path
- `on_word_boundary` callback in `MainFrame` moves the editor insertion point word-by-word as speech proceeds (`wx.CallAfter(editor.SetInsertionPoint, event.offset)`)

**Speech follows focus**
- `is_reading()` added to both `SAPIEngine` (`_chunk_active or _ssml_chunk_active`) and `WindowsTTSEngine` (`_chunk_active`)
- `_restart_speech_from_cursor()` helper: stops current reading and resumes via `speak_from_cursor()` from the new insertion point
- Speech restarts automatically when: cursor moves via mouse click or navigation keys (Left/Right/Up/Down/PgUp/PgDn/Home/End + numpad equivalents); user navigates to a different page; user switches document tabs
- Word-boundary cursor movement does NOT trigger restart (only genuine user navigation)

**Empty-tab replacement on file open**
- `_active_tab_is_pristine()`: detects a single untouched unsaved untitled tab
- `_finish_file_open_inner()` and the fallback raw-load path in `_open_file_in_tab()` both capture the pristine tab index before opening, then delete it after the new document loads successfully
- Behaviour: launch ScanMaster (one "Untitled" tab) → open any file → file replaces the empty tab. Opening a second file while the first is open creates a new tab (first tab is no longer pristine).

### Changed

- App version: `2.3.0` → `2.4.0`

---

## [2.3.0] — 2026-05-24

### Changed — Help System: HtmlHelpController

- Replaced `wx.LaunchDefaultBrowser` with `wx.html.HtmlHelpController` for in-app help
- `_get_help_controller()` lazily initialises the controller from `help/scan_master.hhp`
  and keeps it alive so the help window remembers its position
- `F1` / Help > User Manual → `ctrl.DisplayContents()` — shows TOC panel
- Help > Quick Start → `ctrl.Display("getting_started.html")` — jumps to that section
- Added `import wx.html` to `main_frame.py`
- QA 12.1–12.3 satisfied: F1 opens HtmlHelpController; Quick Start targets correct page

---

## [2.2.0] — 2026-05-24

### Changed — Preferences Listbook

- `PreferencesDialog` rewritten from `wx.Notebook` (3 tabs) to `wx.Listbook`
  (`wx.LB_LEFT`) with **11 category tabs**:
  - **General** — default font, autosave interval, default zoom %, default document language
  - **Appearance** — theme (Light/Dark/System), toolbar style, status bar & sidebar visibility
  - **Languages** — editable list of BCP-47 language entries in SQLite `languages` table
  - **Spelling** — spell-check language, dictionary downloader, as-you-type toggle
  - **Grammar** — enable grammar checking, LanguageTool host/port
  - **OCR** — (existing) engine selection, language code, Tesseract pack installer
  - **Speech** — default engine (SAPI5/WinRT), read-on-move, sentence/paragraph pause;
    "Open Speech Settings…" button
  - **Keyboard** — active profile selector; "Open Keyboard Manager…" button
  - **Autocorrect** — enable, on-space, sentence-case toggles; "Manage Rules…" button
  - **AI** — enable, provider, API key, model, Ollama host
  - **Advanced** — max recent files, backup on save, confirm overwrite, debug logging
- `save_prefs()` extended to persist all 11 tabs to `preferences.db`
- Dialog minimum size increased from 460×380 → 720×520 to accommodate left list panel
- QA 11.1 satisfied: `Ctrl+,` opens Preferences as Listbook; left icon list navigable by
  arrow keys, right panel shows settings for the selected category

---

## [2.1.0] — 2026-05-24

### Added — Phase DOM: Native XML Format, Speech Controls, SSML/SAPI Insertion, Templating & Import/Export

**Document DOM (`scan_master/dom.py`)**
- New `Document > Page > Block > Run` XML DOM with full type annotations
- `PageLayout` dataclass (paper size, margins, orientation, columns, headers, footers)
- `Style` dataclass with `based_on` inheritance chain
- `document_to_xml()` / `document_from_xml()` XML serialiser and deserialiser
- `page_from_rtf()` bridge — converts RICHEDIT50W RTF strings to DOM nodes
- `page_to_rtf()` bridge — renders DOM back to RTF for RICHEDIT50W editing
- Multi-lingual support: `lang` (BCP47) and `direction` (`ltr`/`rtl`/`auto`) on every Run, Block, Page, and Document node

**Native `.smdx` Format**
- ZIP container: `document.xml`, `images/`, `templates/`, `[Content_Types].xml`, `_rels/`
- `save_to_asdx()` / `load_from_asdx()` in `document.py`
- Legacy `.smf` files continue to load and save without modification

**Unified Importer (`scan_master/importer.py`)**
- `import_file()` dispatcher for: `.smdx`, `.smf`, `.epub`, `.docx` (faithful layout via python-docx), `.doc`, `.odt`, `.html`/`.htm`, `.rtf`, `.txt`, `.md` (via Pandoc), `.chm` (via `hh.exe /decompile`), `.pdf` (text or OCR), `.zip` (generic container)
- EPUB importer: parses OPF spine, XHTML pages, images, page-break spans, TOC navigation
- DOCX faithful layout: extracts page size, margins, column count, headers, footers, page breaks, and paragraph/character formatting via python-docx
- ZIP container importer: sniffs format by extension priority; imports each document file as a page

**Unified Exporter (`scan_master/exporter.py`)**
- `export_document()` dispatcher for: `.smdx`, `.smf`, `.epub` (native EPUB 3 — no Pandoc), `.docx` (faithful layout), `.odt`, `.html`, `.rtf`, `.txt`, `.md`, `.pdf`
- Native EPUB 3 exporter: builds full OPF + NCX + nav.xhtml + per-page XHTML + CSS; page numbers preserved via `epub:type="pagebreak"` spans
- Native DOCX exporter: `<w:sectPr>` with page size, margins, columns; headers/footers; page-number fields

**Speech Rate / Volume / Pitch Submenus**
- Speech > Rate: Increase (`Ctrl+]`), Decrease (`Ctrl+[`), Reset, Set Absolute…
- Speech > Volume: Increase (`Ctrl+Shift+]`), Decrease (`Ctrl+Shift+[`), Reset, Set Absolute…
- Speech > Pitch: Increase (`Ctrl+Alt+]`), Decrease (`Ctrl+Alt+[`), Reset, Set Absolute… (SSML prosody)
- All three update status bar with current value after each change

**Insert > Speech Tags (SSML)**
- Prosody, Voice, Emphasis, Break/Pause, Phoneme, Say-As, Language, Mark
- `SsmlTagDialog` — adapts controls to tag type (voice picker, spinboxes for prosody, IPA field for phoneme)
- SSML-tagged runs stored in DOM `Run.ssml_tag` / `Run.ssml_attrs`
- Tagged runs highlighted in editor (light-blue background via `wx.TextAttr`)

**Element-Based Speech Styling**
- New `element_speech_styles` SQLite table (profile_id, element, voice_id, rate, volume, pitch)
- Speech Settings dialog gains "Document Elements" tab with element dropdown, sliders, voice picker, and list of configured elements
- `SAPIEngine.load_element_styles()` / `load_element_styles_from_active_profile()`

**WinRT OneCore TTS Backend**
- `WindowsTTSEngine` class implementing the same `SpeechEngine` protocol as `SAPIEngine`
- `VoiceInfo` dataclass (id, name, lang, engine, gender, is_neural)
- Speech Settings voice tree shows "Windows TTS (OneCore)" branch with ★ on neural voices
- `WindowsTTSEngine.pause()` implemented as stop-and-back-one-chunk with resume

**DOM-Aware SSML Builder**
- `SAPIEngine.speak_page_from_dom(page)` — iterates DOM blocks, builds one `<speak>…</speak>` per block
- `_build_block_ssml(block, doc_lang, page_lang)` — element-style voice/prosody wrappers; per-run `<lang>` tags; run SSML tags; pronunciation substitutions
- Parallel SSML chunk reader (`_ssml_chunk_*` state fields) alongside existing plain-text chunk reader
- `speak_all()` / `speak_page()` route to DOM builder when a DOM is available

**Accessibility Templates (`scan_master/templates/`)**
- `default.xsl`, `screen_reader.xsl`, `low_vision.xsl`, `dyslexia.xsl`, `high_contrast.xsl`
- `TemplateDialog` — lists built-in + custom `.xsl` templates, shows description, Apply/Import/Export
- View > Template submenu (Default, Screen Reader, Low Vision, Dyslexia Friendly, High Contrast, Manage Templates…)

**Format > Language**
- Assigns BCP47 language tag to all blocks on the current page
- SSML builder emits `<lang xml:lang="…">` wrappers for cross-language passages

**Other Improvements**
- `RTF-to-plain` bug fix in `document_view.py` — `_rtf_to_plain()` now handles uppercase control words, hex escapes (`\'XX`), and nested groups; continuous view no longer shows raw RTF markup
- `PageReorderDialog` — proper reorder UI with Up/Down/ToTop/ToBottom buttons (replaces stub)
- `BordersShadingDialog` — two-tab Notebook (Borders + Shading); builds RTF fragment and injects via `_stream_rtf_at_selection`
- `editor.apply_named_style()` — now routes through `StyleRegistry` (was a no-op stub)
- `scan_master.spec` — excludes `torch`, `paddle`, `paddlepaddle`, `onnx`, `tensorflow` from bundle to prevent PyInstaller analysis crashes; build time reduced from hours to ~90 seconds

---

### Added — Phase NEXT: 15 New Editor Features

- **Unlimited Undo/Redo** — `CanUndo()`/`CanRedo()` EVT_UPDATE_UI handlers; menu items grey correctly
- **Paste Plain Text** (`Ctrl+Shift+Alt+V`) — strips formatting from clipboard on paste
- **Paste Special…** — dialog lists available clipboard formats; user selects which to paste
- **Go to Line…** (`Ctrl+Shift+G`) — dialog shows current/total lines; jumps cursor to specified line
- **Bookmarks** — Insert > Bookmark submenu; `bookmarks` SQLite table; Next/Previous (`Ctrl+F2`/`Shift+F2`); Manage Bookmarks dialog
- **Notes/Annotations** — Insert > Note submenu; `notes` SQLite table; Next/Previous; Manage Notes dialog
- **Change Case** — Format > Change Case submenu (UPPERCASE, lowercase, Title Case, Sentence case, tOGGLE CASE / `Shift+F3`)
- **Sort Lines** — Tools > Sort Lines…; ascending/descending, alphabetical/numeric, selected or all lines
- **Date and Time** (`Alt+Shift+D`) — 10+ formats with live preview; timezone selection
- **Equation…** (`Alt+Shift+E`) — Unicode symbol grid (operators, Greek, arrows, fractions, superscripts, subscripts) + LaTeX text input
- **Insert Object…** — Phase 1 informational placeholder (full OLE deferred)
- **Tabs Dialog** — Format > Tabs…; reads/writes `PARAFORMAT2.rgxTabs` via ctypes; Left/Center/Right/Decimal/Bar alignment
- **Section Break** — Insert > Section Break; injects `\sect\sectd\par` RTF
- **Column Break** — Insert > Column Break; injects `\column\par` RTF
- **Comments** — Review menu (new menu between Format and Tools); `comments` SQLite table; yellow highlight on commented ranges; Next/Previous navigation; Manage Comments dialog
- **Clip List** — Tools > Clip List…; `clips` SQLite table; two-panel dialog (list + edit); quick insert (`Ctrl+Shift+Insert`)
- **Edit > Selection submenu** — 6 page-selection modes: Select All (Ctrl+A), Current Page, Previous Page, Next Page, Page Range… (with From/To spinboxes), All Pages, Marked Selection; `PageRangeDialog`
- **Page Marker** — Pages > Set Page Marker (`Ctrl+M`); stored as `(page_index, char_pos)` in MainFrame; used by Marked Selection and OcrRunnerDialog
- **Format > Borders & Shading** — `BordersShadingDialog` with border style/width/colour + shading options

---

### Changed

- App version: `2.0.0` → `2.1.0`
- `build.py` uses `python build.py` (not direct `pyinstaller`); excludes paddle/torch; build time ~90s
- Speech Settings dialog: second tab "Document Elements" added; WinRT voices shown in tree

---

## [2.0.0] — 2026-05-23

### Added — Phase SCAN-3: Scanner Diagnostics, Windows OCR, Continuous View

- WIA HRESULT friendly error messages (`_wia_friendly_error`); one-retry for OFFLINE errors; 30s timeout
- `scan_page_wia` returns `(image, error_str)` tuple
- Windows OCR engine via WinRT `Windows.Media.Ocr` (`ocr_with_windows`, `list_windows_ocr_langs`)
- Continuous document view (`View > Continuous Document`; `Ctrl+Alt+V`) — all pages in one scrollable control with `═══ Page N ═══` separators
- Cursor-at-page-start fix: `SetInsertionPoint(0)` after each page load
- Splash screen drawn programmatically with `wx.MemoryDC`
- Copyright updated to Deenadayalan Moodley; old author-name references removed
- Copyright footer added to all help HTML files

---

## [1.9.0] — 2026-05-22

### Added — Phase SCAN-2: Advanced Scanning, Timed Scan, OCR Runner, PDF Import

- Background scanning threads (non-blocking `ScanDialog`)
- Timed countdown mode (configurable 1–120 s) with auto-restart for multi-page
- `OcrRunnerDialog` — standalone OCR runner with image preprocessing pipeline (deskew, despeckle, contrast, rotate, watermark removal)
- `PdfImportDialog` — method selector (Auto/Text/Tesseract/PaddleOCR) with page count info
- `PageSelectionPanel` reusable widget with 6 modes (Current, Previous, Next, Range, All, Marked)
- Page marker system (`Pages > Set Page Marker`, `Ctrl+M`)
- Regex support in Find/Replace, Autocorrect, and Pronunciation Dictionary dialogs
- Bidirectional speech navigation (previous/next sentence, paragraph, word, line)
- Scan > Recognize Only, Scan Only, Scan and Recognize operation types
- Scan insertion positions (Before, After, Beginning, End)
- Preferences > OCR tab with language pack installer and remove/refresh

---

## [1.8.0] — 2026-04-20

### Added — Phase SCAN-1 + Database Migration

- SQLite3 `DBManager` replaces `wx.FileConfig` / `scan_master.ini`
- Keyboard Manager with full feature registry, profile management, conflict detection
- SAPI5 speech engine with indexed speech, pronunciation dictionaries (4 scopes), pause intervals
- `Scan MasterDocument` / `DocumentPage` model; `.smf` ZIP container (native format)
- `wx.AuiNotebook` multi-tab document management
- `PageSidebar` with thumbnails and slider
- `DocumentView` per-tab widget with image/text/both view modes
- WIA scanner integration — single, ADF, and manual multi-page modes
- OpenCV camera capture with live preview
- Tesseract OCR integration; PaddleOCR integration
- Pandoc import/export (DOCX, ODT, PDF, HTML, RTF, Markdown)
- PyMuPDF PDF import
- `SpeechSettingsDialog` with SAPI voice tree (Engine → Language → Voice)
- Speech profiles — save/load named profiles in SQLite
- `SpellCheckDialog` with as-you-type squiggles via pyenchant
- Grammar check via language_tool_python
- AI assistant dialog (Anthropic Claude, OpenAI GPT, Ollama)
- Dictionary lookup dialog
- Autocorrect (`AutocorrectManager`, CRUD dialog, SQLite storage)
- Full help system (`wx.html.HtmlHelpController`, 9 HTML help pages)

---

## [1.6.0] — 2026-04-04

### Fixed

- Preferences > Spelling: Download button always disabled (language list showed only installed langs)
- Preferences > Spelling: Dictionary install directory crashed on pyenchant 3.x (`utils.get_default_base_dirs` removed in 3.x)

---

## [1.5.0] — 2026-04-04

### Added

- Preferences > Spelling tab: in-app Hunspell dictionary downloader (LibreOffice source, threaded, auto-disable when installed)

---

## [1.4.0] — 2026-04-04

### Added

- Portability foundation: `wx.FileConfig` (`scan_master.ini`), `find_tool()` sidecar pattern, PyInstaller spec
- DOCX/ODT/PDF/CHM import and export
- Image file opening
- WIA scanning and Tesseract OCR

---

## [1.3.0] — 2026-04-04

### Fixed

- Format > Bold/Italic/Underline now fire correctly when RICHEDIT50W has focus (custom IDs bypass wx stock ID routing)
- Format menu check state syncs via `EVT_MENU_OPEN` (not `EVT_UPDATE_UI` which is intercepted by RICHEDIT50W)
- `ctypes.addressof()` overflow on 64-bit replaced with `ctypes.byref()`
- Toggle bold/italic/underline with no selection now sets typing format for next character

---

## [1.2.0] — 2026-04-03

### Added

- Bullets and numbered lists via `EM_SETPARAFORMAT` / `PARAFORMAT2`
- User-creatable named styles (CRUD, persisted in `scan_master.ini`)
- Formatting toolbar font population from system fonts via `wx.FontEnumerator`
- File-type enforcement on Save As (`.rtf` / `.txt` extension always applied)

---

## [1.1.0] — 2026-04-03

### Changed

- Editor replaced: `wx.richtext.RichTextCtrl` → `wx.TextCtrl(style=wx.TE_RICH2)` (native RICHEDIT50W; full UIA/MSAA text-provider support for screen readers)
- Native format changed from custom XML to RTF (RICHEDIT50W native)

### Fixed

- Screen readers did not announce typed characters (custom-drawn RichTextCtrl has no ITextProvider)
- Alt key did not activate menu bar (`WM_SYSKEYDOWN` consumed by RICHEDIT50W)
- Alt+F4 activated menu bar instead of closing
- Save prompt on fresh empty document (RICHEDIT50W fires `EVT_TEXT` during Win32 init)
- Save prompt after typing and deleting all text (`IsModified()` stays `True`)

---

## [1.0.0] — 2026-04-03

### Added

- Initial release: Python + wxPython accessible word processor
- RICHEDIT50W editor, 7 menus, 2 toolbars, status bar
- File open/save (RTF), Find, spell check stub, preferences stub
