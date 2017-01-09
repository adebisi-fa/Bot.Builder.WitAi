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

## Note

Since wit.ai doesn't have **Intent** as a first class feature (as available in Microsoft LIUS), your query must include at least an entity with the name "intent".  

You can then setup a **LuisIntent** attribute with the value of the "intent" entity, in a **LuisDialog** derivative class.  The following example setup a handler for an [wit.ai](http://wit.ai) entity with the name **"intent"**, and value **"register"**:

```c#
public class MyWitAiDialog : LuisDialog<string> {
    public MyLuisDialog() : base(new WitAiLuisService("wit-token-goes-here")) { }
    ...
    [LuisIntent("register")]
    public async Task Register(IDialogContext context, LuisResult result)
    {
        //
        // Retrieve registration information from 'result' parameter.
        // Registration logic goes here
        //
        
        // Report success
        await context.PostAsync($"Registration completed.");
        ...
    }
}
```
