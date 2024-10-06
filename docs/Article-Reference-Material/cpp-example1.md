# C++ Code Formatting Examples

## Codeblock with basic formatting:

An example C++ codeblock with formatting, from src/game/client/ms/hudmusic.cpp. :beer:

```cpp title="src/game/client/ms/hudmusic.cpp" linenums="1"
#include "inc_huditem.h"
#include "sharedutil.h"
#include "clglobal.h"
#include "hudmusic.h"

MS_DECLARE_MESSAGE(m_Music, Music);

int CHudMusic::Init(void)
{
	HOOK_MESSAGE(Music);
	m_MP3.Init();
	return 1;
}

void CHudMusic::Shutdown(void)
{
	m_MP3.Shutdown();
}
```

## Codeblock with line offset start and line highlighting:

An example C++ codeblock with formatting, starting at line #30, and lines 5-13 highlighted, from src/game/client/ms/hudmusic.cpp. :beer: :beer:

```cpp title="src/game/client/ms/hudmusic.cpp" linenums="30" hl_lines="5-13"
int CHudMusic::MsgFunc_Music(const char* pszName, int iSize, void* pbuf)
{
	BEGIN_READ(pbuf, iSize);

	int iCmd = READ_BYTE();
	switch (iCmd)
	{
		case MUSIC_STOP_COMBAT: // stop combat music
		{
			gEngfuncs.Con_Printf("Stopping combat music\n");
			m_MP3.StopCombat();
			break;
		}
		case MUSIC_STOP: // stop combat and area music
		{
			gEngfuncs.Con_Printf("Stopping music\n");
			m_MP3.StopMusic(true);
			break;
		}
		default: // area, combat, or system music
		{
			char* musicFile = READ_STRING();
			//gEngfuncs.Con_Printf(musicFile);
			m_MP3.TransitionMusic(musicFile, iCmd); //sound engine handles the including of dir now.
			break;
		}
	}

	return 1;
}
```

[Documentation for Code Blocks](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/)