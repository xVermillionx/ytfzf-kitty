# ytfzf-kitty
Works only for kitty terminal in Wayland or Xorg

## Edit ytfzf script to use kitty with icat (Wayland|Xorg)

Insert the two lines of code below in the `preview_img` function:

Clears the previous shown image.
```sh
kitty +kitten icat --clear --silent --transfer-mode=stream  
```

Shows the current image.
```sh
kitty +kitten icat --silent --transfer-mode=stream --place=$thumb_width\x$thumb_height@$thumb_x\x$thumb_y $IMAGE  
```

If you want to disable ueberzug you have to comment out the ueberzug functions in `user_selection` :

```sh
user_selection () {

	...

	elif [ "$show_thumbnails" -eq 1 ] ; then 
		dep_ck "ueberzug" "fzf" # dep_ck "fzf"
		# ueberzug_start
	
		...

		# ueberzug_stop

		...

	fi

...

}
```

And remove the check for the $FIFO file in the `parse_opt` function
```sh
U)  preview_img "$optarg"; exit; 
# U)  [[ -p "$FIFO" ] && preview_img "$optarg"; exit; 
```

<!-- ```sh -->
<!-- # Insert in function preview_img -->
<!--   # Clear prev Images -->
<!--     kitty +kitten icat --clear --silent --transfer-mode=stream   -->
<!--   # Disp cur Image -->
<!--     kitty +kitten icat --silent --transfer-mode=stream --place=$thumb_width\x$thumb_height@$thumb_x\x$thumb_y $IMAGE   -->
<!-- ``` -->
