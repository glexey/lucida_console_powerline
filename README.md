# How to patch Windows Lucida Console font for use with Windows gvim + powerline/airline

Need:

1. [fontforge.exe](https://fontforge.github.io/) (font editing suite)
2. [ttx.exe](https://github.com/fonttools/fonttools) (font to/fro XML converter)
3. [powerline-fontpatcher](https://github.com/powerline/fontpatcher) script

Steps:

1. Copy lucon.ttf from /c/windows/fonts to another dir
2. Run powerline-fontpatcher to patch with powerline symbols:

        c:/Program\ Files\ \(x86\)/FontForgeBuilds/bin/fontforge.exe -script ./powerline-fontpatcher lucon.ttf

    Resulting font will not be usable in gvim yet, since it's not marked as fixed pitch.

3. Convert the patched font to XML:

        ttx.exe Lucida\ Console\ for\ Powerline.ttf

4. Edit `Lucida Console for Powerline.ttx` and set `isFixedPitch` to 1:

        <isFixedPitch value="1"/>

5. Convert XML back to ttf:

        rm Lucida\ Console\ for\ Powerline.ttf
        ttx.exe Lucida\ Console\ for\ Powerline.ttx

6. Patched font is ready, drag-n-drop to c:/windows/fonts to install
