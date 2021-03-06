# 3.0.0-beta4

## Added
* `b:AutoPairsJumpRegex`

## Fixed

* Balance checks where the open bracket is regex ([#15](https://github.com/LunarWatcher/auto-pairs/issues/15)) (`count(whatever, open) => s:regexCount(whatever, open)`)
* Manual jump now includes custom pairs

# 3.0.0-beta3

## Added
* `g:AutoPairsMultilineCloseDeleteSpace`
* `g:AutoPairsMultibyteFastWrap` -- fast wrap now supports multibyte pairs
* `g:AutoPairsFiletypeBlacklist`

## Fixed

* Made the vim comment regex less awful
* `AutoPairsMultilineClose` didn't work
* `g:AutoPairsCompleteOnlyOnSpace` regex: \S is enough. Newlines appear to be stripped anyway, so EOL is fine
* Revert `g:AutoPairsMultilineClose` to 0; not sure when it changed to 1
* Corrected multiline pair regex (`'^\V'.close` -> `'\v^\s*\zs\V'.close`); not sure why it was changed in the first place, doesn't appear to be relevant for space-only autoinsert. (Objections are welcome on this one; open an issue if you disagree or if this breaks your use of the plugin)
* Slightly saner check for escaped characters

## Changed
* Made `g:AutoPairsOpenBalanceBlacklist` empty by default. Can't remember the rationale behind adding them in the first place
* [Meta] Removed old, outdated comments and add new confused ones

# 3.0.0-beta2

## Added
* Added `g:AutoPairsVersion`
* Added `g:AutoPairsBackwardsCompat`
* Backwards compat documentation
* Added `g:AutoPairsMultilineFastWrap`; also means minor, optional changes to the fast wrap system
* Added `g:AutoPairsFlyModeList`
* Added `g:AutoPairsJumpBlacklist` ([jiangmiao/313](https://github.com/jiangmiao/auto-pairs/issues/313))

## Fixed
* Incompatibility with vim-visual-multi
* Fixed weird fast wrap behavior when the closer is identical to the opener ([jiangmiao/296](https://github.com/jiangmiao/auto-pairs/issues/296))
* Try to fix issue where brackets are imbalanced on the line, but that isn't indicative of bad balancing. Primarily an issue in multiline if-else blocks, or try-catch blocks in languages like C, C++, and Java. (fix has since been fixed)
* Some function calls were not renamed (bad refactoring; [#13](https://github.com/LunarWatcher/auto-pairs/issues/13))
* Handle strgetchar() returning -1 ([#14](https://github.com/LunarWatcher/auto-pairs/issues/14))
* `g:AutoPairsCRKey` looking for expansions on `<CR>` when `g:AutoPairsCRKey` isn't `<CR>` (should look for keybinds to `g:AutoPairsCRKey` rather than just `<CR>`)
* Update to flymode pairs that unescaped values unescaped ], which _has_ to be escaped.
* Make sure g/b:AutoPairsNoJump = 1 doesn't interfere with balancing logic.

## Changed
* `autopairs#AutoPairsFastWrap` argument movement changed from a required argument to a vararg to make it optional; defaults to `e` when not supplied

# 3.0.0-beta1

## Added
* `autopairs#AutoPairsScriptInit` (dummy function for autoload; see the docs)
* `g:AutoPairsLanguagePairs` (exposed previously private API)
* `g:AutoPairsAutoLineBreak`
* `g:AutoPairsCarefulStringExpansion`, `g:AutoPairsQuotes`

## Fixed
* Load autopairs functions properly (switch primary script to autoload)
* Jump keybind and backticks ([jiangmiao/299](https://github.com/jiangmiao/auto-pairs/issues/299))
* Moved variables from the wrong section of the help document to the right section. Whoops!
* Make `g:AutoPairsOpenBalanceBlacklist` work (+ add docs)

## Changed
* Merged `b:AutoPairs` help into `g:AutoPairs`
* Added notice of the existence of a buffer variable for (hopefully) all the variables that have a buffer variant.
* Moved the movement logic in `autopairs#AutoPairReturn()` to a separate function to enable `g:AutoPairsAutoLineBreak`

# 3.0.0-alpha4

## Added
* `g:AutoPairsSearchCloseAfterSpace`
* `g:AutoPairsSingleQuoteMode`
* `g:AutoPairsSingleQuoteExpandFor`

## Fixed
* `g:AutoPairsNoJump` didn't work as intended; this has now been fixed. An if-statement in the wrong place prevented it from doing what it was meant to do; avoid jumping.
* Typo in AutoPairsDelete causing backspace errors
* Bad backslash use in character group ([#10](https://github.com/LunarWatcher/auto-pairs/pull/10))

## Changed
* Corrected documentation of AutoPairsDefine to include the optional second argument.

# 3.0.0-alpha3

## Changes
* AutoPairsFastWrap now has a parameter that decides the movement. The one mapped by default is `e`, but due to how Vim works, the argument has to be passed explicitly. (Vim 8.1 patch 1310 supports default arguments in functions, but anything before that as well as neovim would lose support). ([#8](https://github.com/LunarWatcher/auto-pairs/pull/8))

## Fixed
* `AutoPairsDefine` called `AutoPairsDefaultPairs` without `autopairs#` (missed part of the breaking change from 3.0.0-alpha2)
* Prevent issues when removing a key that doesn't exist in `AutoPairsDefine` ([#9](https://github.com/LunarWatcher/auto-pairs/pull/9))
* Fix comment regex for vimscript files ([#7](https://github.com/LunarWatcher/auto-pairs/pull/7))


# 3.0.0-alpha2

## Added
* `g:AutoPairsNoJump`
* `g:AutoPairsDirectoryBlacklist`
* `g:AutoPairsCompleteOnSpace`
* `g:AutoPairsInitHook`
* Added function documentation
* Added multibyte pair documentation
* Document `b:autopairs_enabled`
* Add more buffer variants of variables

## Changes
* [Breaking] Moved all autopair functions to have an `autopairs#` prefix

## Fixes
* Clarified the addition of pairs
* Cleaned up the define cascades with a function (3 lines -> 1 line)
* Fixed pair regex in vimscripts to better detect when quotes are likely to be comments. Largely [#7](https://github.com/LunarWatcher/auto-pairs/pull/7) (thanks to [lemeb](https://github.com/lemeb)!), but with a minor change to ignore Plug, Plugin, echo, and echoerr (where you can use double-quotes for strings, but these commands cannot have a comment on the same line -- Vimscript is weird). The changes ignoring those four commands are hackish -- improvements are welcome.

# 3.0.0-alpha1

Initial release of this fork; primarily fixes a few bugs, contains documentation updates, and merges a few pull requests of varying sizes. The changelog wasn't added until 3.0.0-alpha2, which means the changes here weren't properly tracked.

