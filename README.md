<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTzv-Q5bGIZLgsedVq7yCCAQo3fEC95bUeSM_foUjpX8z1XCtDy1kFL3DqHAhKzKcpSdUY"/>

# rust_console_loading
<img src="https://media.discordapp.net/attachments/1045473607305941053/1136219569963405412/pic-full-230802-1449-49.png?width=1076&height=605"/>

```rs
use std::{thread, time::Duration};


fn main() {
    lala('🦀', '🔸', "right ");
}

fn check_move(mut move_dir: &str) -> &str{
    match move_dir {
        "right "  => move_dir = "bottom",
        "bottom"  => move_dir = "left  ",
        "left  "  => move_dir = "top   ",
        "top   "  => move_dir = "right ",
        _ => println!("lala")
    };
    move_dir // here gona return new dir
}

fn lala(b0: char, b1: char, mut move_dir: &str) {
    print!("\x1b[2J");
    
    let hight: i32 = 7; // here is map size
    let width: i32 = hight; // here is take map hight to width
    let mut h: i32 = 0; // here is postion start of ( x )
    let mut k: i32 = 0; // here is postion start of ( y )

    loop {
        // clear command whit out delete every thing just change
        print!("\x1b[H");

        // here gona print coordinates and the movement direction 
        println!("+-----------+",);
        println!("| ~> h: {}   |", h);
        println!("| ~> k: {}   |", k);
        println!("| ~> {} |", move_dir);
        println!("+-----------+",);

        // this is loop for map using hight and wodth 
        for y in 0..hight  {
            for x in 0..width  {
                // here gona draw map and player postion
                if x == h && y == k {
                    print!("{}", b0);
                } else {
                    print!("{}", b1);   
                }
            }
            print!("\n");
        }

        // check movement direction 
        match move_dir {
            "right " => h +=1,
            "bottom" => k +=1,
            "left  " => h -=1,
            "top   " => k -=1,
            _ => println!("The move_dire does not satisfy any of the written conditions"),
        }

        // take turn
        if move_dir == "right " && h >= width   {
            move_dir = check_move(move_dir);
            h = width-1;
            k +=1;
        }
        if move_dir == "bottom" && k >= hight-1  {
            h =width-1;
            move_dir = check_move(move_dir);
        }
        if move_dir == "left  " && h <= 0  {
            move_dir = check_move(move_dir);
        }
        if move_dir == "top   " && k <= 0  {
            move_dir = check_move(move_dir);
        }

        
        thread::sleep(Duration::from_millis(100));
    }
}
```
