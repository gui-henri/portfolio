---
titulo: "Visualizing BFS - A code challenge"
id: '98_visualization'
descricao: "How i used Go and Raylib to learn more about different pathfinding algorithms."
layout: ../../../layouts/PostLayout.astro
---

I once had an algorithm class in college. There, i saw many approaches that could be used to solve countless problems. It was nice, but it turned out being boring. The main reason behind this lied on my teacher, that tried to make me learn dozens of algorithms and how they work, but not even once talked about how they were implemented.
<br>
<br><i>What is a hashmap?</i><br><br>
Oh is just when you throw a value into an hash function and then store it accordingly. <br><br><i>Great, now how you would implement it?</i><br><br>
Eh...<br><br>
I just couldn't. It was all up to me if i wanted to learn those things. Truth is, not a single soul would encourage me to do that. Most of my college friends are now employed, and none of them remember what a red-black tree is useful for. I'm pretty convinced that i don't need that to survive this world, but still, the thought that i <i>can't</i> do it, even if i wanted, haunted me. So i decided that it was my turn to implement a cool algorithm and make a video about it.

<h2 className="text-2xl font-bold mt-9 mb-9">The initial thoughts.</h2>

I knew i could do just a terminal based app in python and call it a day. I knew i could use any game engine to render graphics. But i'm a masochist and i was ready for a challenge. I saw a Tsoding stream using Raylib and i thought it would be a good idea to use it. In Go, of course, because i use windows, and i hate C++ on windows.
<br><br>
To my luck, just recently the Go bindings of Raylib received an update. Now, you don't have to recompile Raylib everytime you compile your program, you can type [```set cgo_enabled=0```] on your terminal and paste the Raylib .dll into your project folder. It was that easy to setup everything, i was ready to action. 
<br><br>
Chosing what algorithm to implement was also easy, but the story behind it is very interesting. During one of the classes, the teacher started to belabor about A* algorithm. He talked a lot about the math behind it and how it could be used to solve a rubik's cube. It was a shame thought, that he forgot to teach how it worked (to be fair, he mentioned an heuristic function, but only in a vague and mathematical way).
<br><br>
Some weeks later, i found a video on Youtube showing a pathfinding visualization using A*, and instead of finding it funny, i was filled with rage. Why the teacher didn't showed something like this? I would have comprehended it much better than with that crazy math. Not to mention that by looking the video, i could clearly have an idea of how it would be implemented. That night, i picked up my pride and said to myself: "i'm going to make that shit".
<br><br>
<i>In the article, i asume you know what A* is. If you don't, worry not! Here's the wikipedia page for that: <a href="https://en.wikipedia.org/wiki/A*_search_algorithm" class="text-blue-500" target="_blank">A* Algorithm</a></i>

<h2 className="text-2xl font-bold mt-9 mb-9">The workings.</h2>

The first thing i did was to draw a square. Then, i drew some more. And then, i added ui (using raygui) to set the number of squares on the screen. It sounds easy, and it was. Raylib is amazing, and i can't praise it enough by how straightfoward it is. In only a few minutes, i felt like a senior doing magic. 
<br>
<br>
```go
    func main() {
        rl.InitWindow(screenWidth, screenHeight, "Test Window")
	    defer rl.CloseWindow()

        rl.SetTargetFPS(60)

        for !rl.WindowShouldClose() {
            // app logic here

            rl.BeginDrawing()
            {
                rl.ClearBackground(rl.Black)

                // draw objects here
            }

            rl.EndDrawing()
        }
    }
```
<br>
<br>
Despite that, i had some problems when combining it with Go. First we have the type conversions. God, you need to make so many of then. It may be a skill issue, and it wasn't hard to fix, but it sure got my nerves. Second, the performance is really behind the original C version, probably because it goes back and forth between the two languages. It may be a skill issue as well. Also, building the UI was fairly easy, despite bad documentation on raygui for Go.
<br>
<br>
Right after that, i added the square painting functionality, meaning that i was ready to implement A*. Here, something funny happened: i accidentally implemented BFS in a very clever way. Just before implementing the heuristic function for the A* to work, i added a piece of code like this as a placeholder:
<br>
<br>

    func (g *Grid) calculateScore(c *Cell) float64 {
        return c.score + 1
    }

```

```````
<br>
<br>
Not expecting much, i hit play and saw it working first time. I remember stoping for a moment and trying to think why this worked. Realization only came later, that by adding one to the score of each cell in the frontier (i'm calling the squares "Cells", and the frontier are the cells adjascent to the initial cell), checking every single one of then, adding 1 again to each neighbor and repeating was the same as a BFS. I was really happy, because now i could say i implemented two algorithms, when i was only trying to implement one. By it's nature, BFS aways gives the best result, so it also worked as a benchmark about the speed and performance of the A*.
<br>
<br>
Some bugfixes later, i had the A* working as well. It was tricky because of how bad my code was organized, but i was able to solve it. Overall, the experience was great. I was finally able to learn how the algorithm worked under the hood and i still managed to learn some Raylib in the proccess! As final touch, i added sounds for each step of the algorithm and recorded some videos. Here's the BFS one, which sound the best.
<blockquote class="twitter-tweet" data-media-max-width="560"><p lang="en" dir="ltr">I made this pathfinding algorithm visualizer in Go and Raylib. I have no idea on how i should post this on linkedin lol. I&#39;m so happy that it works. <a href="https://t.co/vWv5kRSWui">pic.twitter.com/vWv5kRSWui</a></p>&mdash; Guilherme Henrique (@Astrobio_) <a href="https://twitter.com/Astrobio_/status/1744408808397357466?ref_src=twsrc%5Etfw">January 8, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
