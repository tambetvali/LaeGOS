# LaeGOS
This is Laegna Calculator Operating system.

[Laegna Lane](https://github.com/tambetvali/LaeLane/) is the new challenge for Laegna and Spireason.

I created tasks for handheld calculator input, showing Laegna Lanes and Latin Lines in various formats out of the numbers.
- Initial versions are perfect in that they fully resemble visualizations in my head, when thinking of Laegna math.
  - This is simplified, and sometimes lacks clear, rigid number preciseness:
    - Most textbooks contain vague illustrations for topics such as exponents, such as envisioning accelerating growth and not exact functions.
    - Many maps are topologically distorted to reflect the content better and gain logic.
    - I decided the AI decisions were successful for initial introduction.
   
The problem is we do not need just initial introduction.

***LaeGOS*** will be **Laegna Haldheld Calculator Operating System** and we will implement the following environment:
- Laegna online system, which looks like operating system - it has windows, task bar, and start menu.
- In initial versions, it remembers one number, which is the calculator context (calculator typically has it's whole state in one number, and allows single operations):
  - If keyboards are opened, they can change the number from perspective of various bases.
  - If calculator screens are opened, they can have different formats and bases and display interests.
  - If graphics and visualizations are opened, they demonstrate something about current number.

This is simple, yet powerful way to do it.

## Platform selection for LaeGOS

These are specifications for platform:
- [https://www.pythonanywhere.com/](https://www.pythonanywhere.com/) - this is the free hosting service, which supports Python and Flask.
- [https://laegna.pythonanywhere.com/](https://laegna.pythonanywhere.com/) - this is where LaeGOS will appear.
- [WinBox.js](https://nextapps-de.github.io/winbox/) kind of JS environment - this is currently unknown.
Programming language and environment:
- [Python](https://www.python.org/) - programming language.
- [Flask](https://flask.palletsprojects.com/en/stable/) - server.

I will update about JS environment: like given example, it supports windows.
