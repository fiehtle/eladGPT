<p><a target="_blank" href="https://app.eraser.io/workspace/rF1N6GgdOFXlIS241MVK" id="edit-in-eraser-github-link"><img alt="Edit in Eraser" src="https://firebasestorage.googleapis.com/v0/b/second-petal-295822.appspot.com/o/images%2Fgithub%2FOpen%20in%20Eraser.svg?alt=media&amp;token=968381c8-a7e7-472a-8ed6-4a6626da5501"></a></p>

# eladGPT
This is an implementation of Mayo's code for Langchain + Supabase. I tweaked the UI and introduced shadcn + feed Supabase vector db full with the knowledge of Elad Gil. 

[﻿Tutorial video](https://www.youtube.com/watch?v=prbloUGlvLE) 

[﻿Get in touch via twitter if you need help](https://twitter.com/mayowaoshin) 

The visual guide of this repo and tutorial is in the `visual guide` folder.

## Development
1. Clone the repo
```
git clone [github https url]
```
1. Install packages
```
pnpm install
```
1. Set up your `.env`  file
- Copy `.env.local.example`  into `.env` 
Your `.env`  file should look like this:
```
OPENAI_API_KEY=

NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```
- Visit [﻿openai](https://help.openai.com/en/articles/4936850-where-do-i-find-my-secret-api-key)  to retrieve API keys and insert into your `.env`  file.
- Visit [﻿supabase](https://supabase.com/)  to create a database and retrieve your keys in the user dashboard as per [﻿docs instructions](https://supabase.com/docs) 
1. In the `config`  folder, replace the urls in the array with your website urls (the script requires more than one url).
2. In the `utils/custom_web_loader.ts`  inside the `load`  function replace the values of `title` , `date`  and `content`  with the css elements of text you'd like extract from a given webpage. You can learn more about how to use Cheerio [﻿here](https://cheerio.js.org/) 
You can add your custom elements to the metadata to meet your needs, note however that the default loader format as per below expects at least a string for `pageContent` and `metadata` that contains a `source` property as a returned value:

```
async load(): Promise<Document[]>{
const $ = await this.scrape();
    const text = $("body").text();
  const metadata = { source: this.webPath };
  return [new Document({ pageContent: text, metadata })];
}
```
The `pageContent` and `metadata` will later be stored in your supabase database table.

1. Copy and run `schema.sql`  in your supabase sql editor
- cross check the `documents`  table exists in the database as well as the `match_documents`  function.
## 🧑 Instructions for scraping and embedding
To run the scraping and embedding script in `scripts/scrape-embed.ts` simply run:

`npm run scrape-embed` 

This script will visit all the urls noted in the `config` folder and extract the data you specified in the `custom_web_loader.ts` file.

Then it will use OpenAI's Embeddings(`text-embedding-ada-002`) to convert your scraped data into vectors.

## Run the app
Once you've verified that the embeddings and content have been successfully added to your supabase table, you can run the app `npm run dev` and type a question to ask your website.

## Credit
Frontend of this repo is inspired by [﻿langchain-chat-nextjs](https://github.com/zahidkhawaja/langchain-chat-nextjs) 

This repo uses in-depth Notion guides from the [﻿website](https://thomasjfrank.com/) of productivity expert, Thomas Frank.


<!--- Eraser file: https://app.eraser.io/workspace/rF1N6GgdOFXlIS241MVK --->