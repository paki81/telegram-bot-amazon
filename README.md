This is a Telegram bot that, if made admin of a group, will delete any message
containing an Amazon link and re-post it tagged with the specified affiliate tag.

It can be either messaged directly, or added **as an administrator** to a group or supergroup.

If messaged directly, it replies with the affiliate link, while in a group it will delete any message containing an Amazon link and replace it with a new message, with a format that is customizable through the `GROUP_REPLACEMENT_MESSAGE` environment variables.

## Configuration

It requires two parameters through environment variables:

* `TELEGRAM_BOT_TOKEN` (required) is the token obtained from [@Botfather](https://t.me/botfather)
* `AMAZON_TAG` (required) is the Amazon affiliate tag to be used when rewriting URLs.

You can set two optional parameters through environment variables:

* `AMAZON_TLD` is the Amazon TLD for affiliate links (it defaults to "com", but you can set it to "it", "de", "fr" or whatever)
* `GROUP_REPLACEMENT_MESSAGE` specifies the format for the message that gets posted to groups after deleting the original one. If not set, it will default to `Message by {USER} with Amazon affiliate link:\n\n{MESSAGE}`. In the following table you'll find variables you can use.

| String               | Replacement                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `{USER}`             | The user that posted the message, as `@username` if they created a Telegram username, as `first_name last_name` otherwise. |
| `{ORIGINAL_MESSAGE}` | The user's original message, with no replacements (so it will contain the non-affiliated Amazon link).                     |
| `{MESSAGE}`          | The user's message, with the affiliated Amazon link the bot created.                                                       |

## Running the app

You can either run the app directly through NodeJS

    TELEGRAM_BOT_TOKEN=your-token AMAZON_TAG=your-tag node index.js

Or you can run it in Docker

    docker run -e TELEGRAM_BOT_TOKEN=your-token -e AMAZON_TAG=your-tag --init lucatnt/telegram-bot-amazon

Note that the `--init` option is highly recommended because it allows you to stop the container through a simple Ctrl+C when running in the foreground. Without it you need to use `docker stop`.
