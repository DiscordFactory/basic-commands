# 📦 Message commands
The [Discord Factory](https://github.com/DiscordFactory/factory) framework no longer includes the use of commands via the `messageCreate` event by default.

The `@discord-factory/message-commands` module allows you to restore the use of these commands.

In order to use the module, you need to take the following steps:
```bash
npm install @discord-factory/message-commands
# or
yarn add @discord-factory/message-commands
```

Add the module to the plugins in the `App/start/Kernel.ts` file:
```ts
import BasicCommands from '@discord-factory/basic-commands'

export default class Kernel {
  public registerAddons () {
    return [BasicCommands] 👈 // Do not instanciate it
  }
}
```

You can generate a command file by using the command below:
With NPM
```
npm run factory make:message-command MyCommand
```
With YARN
```
yarn factory make:basic-message MyCommand
```

Now you will need to add 2 keys to your environment file :
```yaml
MESSAGE_COMMANDS:
  APP_PREFIX: Your prefix
  COMMAND_AUTO_REMOVE: true # or 'false'
```
```json
"MESSAGE_COMMANDS": {
  "APP_PREFIX": "Your prefix"
  "COMMAND_AUTO_REMOVE": true // or 'false'
}
```

Once added, you can now create your orders with this minimal structure
```ts
import { Command, BaseCommand } from '@discord-factory/basic-commands'
import { Message } from 'ioc:factory/Discord/Event'

@Command({
  label: 'Foo command',
  description: 'Foo description',
  tag: 'foo'
})
export default class FooCommand extends BaseCommand {
  public async run (message: Message, args: string[]): Promise<void> {
    // Your code here
  }
}
```

## License

[MIT](./LICENSE) License © 2021 [Baptiste Parmantier](https://github.com/LeadcodeDev)
