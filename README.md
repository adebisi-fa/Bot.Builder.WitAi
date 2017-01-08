# Bot.Builder.WitAi
Wit.ai integration with Microsoft Bot Builder LuisDialog.  It implements the Bot Builder ILuisService.

## Installation
```
Install-Package Adfa.Bot.Builder.WitAi
```

## Usage

```c#
[Serializable]
public class MyLuisDialog : LuisDialog<string> {
    public MyLuisDialog() : base(new WitAiLuisService("wit-token-goes-here")) { }
    
    [LuisIntent("")]
    public async Task None(IDialogContext context, LuisResult result)
    {
        await context.PostAsync($"Sorry I couldn't process that expression.");
        // ...
        // Close dialog and return to parent
        context.Done(result?.Query);
    }
}
```
