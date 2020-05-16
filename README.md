# Demo steps showing IntelliJ features
1. Create `src/main/java/Main.java` with `public static void main(String[] args)` and have git skip the file
1. Use **Shift+F6** to refactor class name to `PdfReaderExample`
1. Add `package com.yang.andy.example` and use **Alt+Enter** to move package to correct spot
1. Add `File file = new File("./src/main/resources/muchado.pdf");` and use **Alt+Enter** to import package
1. Add `PDDocument document = PDDocument.load(file);` and use **Alt+Enter** to import package
1. Use **Alt+Enter** on `load()` to add exception to method signature
1. Type `PDFTextStripper p` and select a varname from the suggestions
1. Hit **Alt+Enter** to import the class, then add `new PdfTextStripper();`
1. Go to **View -> Tool Windows -> Git**, and drag+drop `Main.java` into the Default Changelist
1. Right-click `Main.java` and commit using interactive menu
1. Add a `document.close()` to the end (no leaks here!)
1. Go to **VCS -> Commit** and review changes to `Main.java`
1. Check the Amend box this time, then Commit
1. Add `String text = pdfTextStripper.getText(document);`
1. Add following block of code:
    ```
    Pattern kindPattern = Pattern.compile("\\b(kind)\\b", Pattern.CASE_INSENSITIVE); Matcher kindMatcher = kindPattern.matcher(text); int kindCount = 0;
    
    while (kindMatcher.find()) { kindCount++; } System.out.println(kindCount);
    ```
1. Hit **Ctrl+Alt+L** to format the lines just added
1. Run the program to see the results!
1. Highlight from `Pattern kindPattern` to the end of the `while` block, right-click, **Refactor -> Extract Method** and generate a new package-private method `wordCounter`
1. Right-click the new method name, choose **Refactor -> Change Signature**, and add the parameter `String wordToCount` with default value `kind`
1. Update the method with the below code:
    ```
        String expression="\\b"+wordToCount+"\\b";Pattern wordPattern=Pattern.compile(expression,Pattern.CASE_INSENSITIVE);
        Matcher wordMatcher=wordPattern.matcher(text);return wordMatcher.results().count();
    ```
1. Hit **Ctrl+Alt+L** as before, and run.
1. Hit **Ctrl+Alt+T** and generate a new test for `wordCounter()`.
1. Paste the following code into the test:
    ```
        String testString="actual actual actual actual actual subject";long actual=Main.wordCounter(testString,"actual");assert(actual==5);
    ```
1. Hit **Ctrl+Alt+L** as usual, and then hit **Ctrl+Alt+O** to clean up your unused imports.
1. Open up the Git panel again, and click into the Log tab. Right-click on the commit for `init gradle project`, then choose **New Branch**.
1. Commit current changes to the new branch, then checkout `master` again and replace `Main` with the below code:
    ```
        String text = "MyText";
        String textTwo = "AndNewerText";
        System.out.print("myLatestTextIs" + text + textTwo);
    ```
1. Hit **Ctrl+Alt+O** to clean up now-unused imports, and commit to `master`.
1. Open up the Log tab of Git again, right-click the new branch and **Merge into Current**.
1. Resolve the merge conflict using IntelliJ's panel.

# Miscellaneous Niceties
* IntelliJ can do way more than just commit and merge for you: undo is a useful one, as is push/pull.
* Scratch files are really nice ways to keep notes, and automatically steal your clipboard on creation.
* IntelliJ debugging is for another time, but I'd recommend doing some reading. If you ever try it, look for the **Evaluate Expression** option.

# Summary
* **Alt+Enter** is your best friend.
* IntelliJ offers some great Git niceties! (But knowing how git works is REALLY important before using it.)
* If you don't remember the shortcut, **Ctrl+Shift+A** gets you there.
