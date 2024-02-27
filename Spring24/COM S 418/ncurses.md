```
void init_terminal(void) {
	initscr();
	raw();
	noecho();
	curs_set(0);
	keypad(stdscr, TRUE);
	start_color();
	init_pair(COLOR_RED, COLOR_RED, COLOR_BLACK);...
	1st is the name, 2nd is the txt color, and 3rd is background color
}
```