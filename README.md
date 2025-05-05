<div align="center">

# ᴛʜᴇ <span data-block="procedure">ᴍɪsᴛ</span><span data-block="variable">ᴘʀᴏᴊᴇᴄᴛ</span>
*An effort to bring syntax to App Inventor to enable deeper tooling and code analysis*
</div>

<hr>

### 𝗧𝗔𝗕𝗟𝗘 𝗢𝗙 𝗖𝗢𝗡𝗧𝗘𝗡𝗧𝗦

1. *Preface*
2. *The Mist Architecture*
3. *The Mist Programming Language*
4. *The Code Editor*
5. *Open Source*
6. *About*

<hr>

### 𝗣𝗥𝗘𝗙𝗔𝗖𝗘

App Inventor originally did not have syntax for its blocks, which made linting or other code analysis harder to implement into the IDE.

Additionally, as the world embraces LLMs for code assistance, App Inventor faces a challenge. LLMs rely on syntax to understand and analyse code effectively.

My research project aims to cut short these disadvantages to envision an App Inventor IDE filled with much better tooling and code analysis.

<hr>

### 𝗧𝗛𝗘 𝗠𝗜𝗦𝗧 
𝗔𝗥𝗖𝗛𝗜𝗧𝗘𝗖𝗧𝗨𝗥𝗘

![image|690x230](upload://8uYXpFCFaDPlpIfWBr1llA38tlg.png)
<div align="center"> 

*Engineering of the Mist Architecture*
 </div>
<br>

1.  **Generic Blockly Transformer**

     Written in Kotlin, can transform over 270+ manually mapped unique blocks, from Blockly XML to an intermediate representation for further syntax construction.

     This allows the translation of App Inventor blocks to any programming language i.e. loosely typed (*Mist, Python, JS*).

2. **Mist Transpiler**

    Generates Mist code from the intermediate Blockly representation.
   The syntactical output can then be fed into LLMs for code analysis and assistance.

   Opens up a possibility, where the LLMs generate Mist code that can later be converted into blocks.

3. **Lexer** (*internal*): Performs [Lexical analysis](https://en.wikipedia.org/wiki/Lexical_analysis) on Mist code.

4. **Parser**

   Constructs meaningful ASTs (*[Abstract Syntax Trees](https://en.wikipedia.org/wiki/Abstract_syntax_tree)*) from the Lexical output.

   This allows static analysis techniques to be applied such as:

   -  *Dynamic Type Resolution*: Pre-determining the possible data types, a piece of code or procedure may return to prevent writing code that always fails.
   -  *Redundancy testing*: Identifying redundant codes, such as if-conditions or blocks, that never execute, always execute, always fail or always succeed.

5. **Multi-Platform Execution**

   The Mist Programming Language is written in pure Java 7, allowing it to run anywhere! Android, Desktop and even locally in your browser — using technologies such as [TeaVM](https://www.teavm.org/).

   Almost all of the Built-In blocks have been re-implemented in the language, trying to mimic 1:1 behavior. Although distortions are imminent.

<hr>

### 𝗧𝗛𝗘 𝗠𝗜𝗦𝗧
𝗣𝗥𝗢𝗚𝗥𝗔𝗠𝗠𝗜𝗡𝗚 𝗟𝗔𝗡𝗚𝗨𝗔𝗚𝗘

Crafted with syntax to suit App Inventor's needs and functional programming style.

Mist is left to right parsed language, i.e. no high precedence operations. <kbd> !( <span data-block="variable"> +-</span>  < <span data-block="variable"> */ </span>    )</kbd>

*Support for blocks at execution:*

1. *Fully supported*
     <span data-block="logic">**Logic**</span>, <span data-block="math">**Math**</span>, <span data-block="text">**Text**</span>, <span data-block="color">**Colors**</span>, <span data-block="list">**Lists**</span>, <span data-block="variable">**Variables**</span>, <span data-block="procedure">**Procedure**</span>

2. *Partially supported*

   - <span data-block="control">**Control**</span> blocks are fully supported, except app specific blocks such as <span data-block="control">Close Screen</span>, <span data-block="control">Close App</span>, <span data-block="control">Get Start Value</span> ... etc.

   - <span data-block="dictionary">**Dictionary**</span> blocks are fully supported, but untested for faulty implementations (*dictionary walk blocks*)

3. *Redundant; Syntax only support*

   - **Components**, **Events**, and **Properties**

<hr>

### 𝗧𝗛𝗘 𝗖𝗢𝗗𝗘 𝗘𝗗𝗜𝗧𝗢𝗥

![MistCodeEditor|video](upload://2K7ZswqtIrXPt9Pj2znC4nW7rBj.mp4)

<div align="center">

*The Mist Code Editor and Live testing Environment*

</div>

<br>

The code editor offers live block-to-syntax conversion and a way to live-test non-application blocks on the go. It's a *magic* *Do-It functionality* that happens on your browser locally :wink:.

<kbd>Try it out! :globe_with_meridians: [mist.ekita.me](https://mist.ekita.me)</kbd>

> **!** *The server and syntax conversion might be slow depending on where you are in the world.* 

>  **!** *This is a constantly evolving project. Trying out the editor is the best way to learn syntax.*

*A few tips to work with the editor*

-  Clicking on the workspace shows only the syntax of top blocks (*Global Variables, Procedures, and Events*), orphaned blocks are ignored.

-  Do not leave empty sockets, they result in syntax conversion failure.

-  Hold shift to select multiple blocks — to run a procedure, select the procedure itself and the call block.

-  Any manual edits on the editor are discarded.

- You may run into a few errors while testing, do check out your browser's console.

*The syntax conversion happens on the cloud (due to high level Kotlin) and the execution locally on your browser (JS).*

<hr>

### 𝗢𝗣𝗘𝗡 𝗦𝗢𝗨𝗥𝗖𝗘

The project is licensed under Apache 2.0.

- *[Mist](https://github.com/XomaDev/Mist)*: The Mist Programming Language core
- *[juiceBlocklyXML](https://github.com/XomaDev/juiceBlocklyXML)*: Generic blockly transformer and Mist transpiler.
- *[JS Addon](https://github.com/XomaDev/MistAI)*: Code editor and live testing
- *[Code Editor iFrame](https://github.com/XomaDev/MistPlayground)*: Syntax highlithing tuned for Mist

<hr>

### 𝗔𝗕𝗢𝗨𝗧

I had a good time working on this project half-summer. I have a lot of ideas in my mind. 

Currently, I'm done with the Block Syntax conversion and live testing environment... Eventually, we'd need to do the reverse (Syntax to Block conversion), which would be a step closer to LLM integration and linting.

Need to also balance other of my work... Let's see how far we can get this summer before my pre-university (high school) starts.

<hr>

Thank you
*Built with Love and Passion*

Kumaraswamy B G
*a 17 year old*
