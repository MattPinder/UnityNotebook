\# Miscellaneous tips from Unity's 2D guides



\## Tips from \[2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3)



\### \[Layer Collision Matrix](https://learn.unity.com/course/2d-beginner-adventure-game/unit/characters-and-interaction-mechanics/tutorial/implement-projectiles-for-the-player?version=2022.3#64d4f752edbc2a6ed17e1cc8)

A simple way to specify which layers should or shouldn't interact with one another. This is useful if you want e.g. projectiles not to interact with tilemap colliders

1. Set any relevant objects' \*\*Layer\*\* in the Inspector, creating new layers as appropriate
2. Go to \*\*Edit > Project Settings > Physics 2D\*\*, and select the \*\*Layer Collision Matrix\*\* tab
3. Disable any cells corresponding to layers that you \*\*don't\*\* want to interact with each other
