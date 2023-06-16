[![trophy](https://github-profile-trophy.vercel.app/?username=JohnnyJumper)](https://github.com/ryo-ma/github-profile-trophy)
# Hi there 👋

I'm Johnny, ex Physics teacher, currently a passionate developer, future philantropist (hopefully).

## 🔭 I’m currently working on ...

- **rusty-bot**: Simple discord server bot that holds "reputation" value for each member of a guild and gives those members api to change each other's reputation, query the messages and times. All in rust lang
- **airecruter**: an LLM based Algorithm to ease out a job search
- **driver.app**: Startup to conquer the ridesharing industry by storm.

## 🌱 I’m currently learning ...

- Rust
- Blockchain
- Web3

## 💬 Ask me about ...

- Anything related to C or TypeScript, front end or backend.
- Blockchain and decentralized applications
- Any interesting idea to work on? [ I am an idea generator and can help with some creative brainstorms ] 

## 📫 How to reach me ...

- Email: jeyhunt@gmail.com
- LinkedIn: https://www.linkedin.com/in/johnyvolt

## ⚡ Fun fact ...

- I love playing chess and play video games
- I'm a big fan of Witcher universe
- I can speak three languages: English, Russian, and Azerbaijani

## 📄 Some of my code snippets ...

```c
// ft_printf.c

#include "ft_printf.h"

int	ft_printf(const char *format, ...)
{
	va_list	args;
	int		len;

	va_start(args, format);
	len = ft_vprintf(format, args);
	va_end(args);
	return (len);
}
```

```ts
// Custom fetch Provider for UD resolution.ts

import { Provider } from './types';

export class FetchProvider implements Provider {
  private readonly url: string;

  constructor(url: string) {
    this.url = url;
  }

  public async request(request: RequestArguments): Promise<unknown> {
    const response = await fetch(this.url, {
      method: 'POST',
      headers: { 'content-type': 'application/json' },
      body: JSON.stringify(request),
    });

    if (!response.ok) {
      throw new Error(`FetchProvider: ${response.status} ${response.statusText}`);
    }

    return response.json();
  }
}
```

<!--
**JohnnyJumper/JohnnyJumper** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
