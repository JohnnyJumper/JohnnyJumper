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

- I love playing chess and video games
- I'm a big fan of Witcher universe
- I can speak three languages: English, Russian, and Azerbaijani

## 📄 Some of my code snippets ...

```ts
// Resolution.ts

import { ResolutionError, ResolutionErrorCode } from './errors/resolutionError';
import { NamingServiceName, SourceDefinition, SourceParameters } from './types/publicTypes';
import { constructRecords, isNullAddress } from './utils';
import { EthereumNamingService } from './namingServices/ethereum';
import { Zns } from './namingServices/zns';
import { Ens } from './namingServices/ens';
import { Cns } from './namingServices/cns';
import { Udapi } from './namingServices/udapi';
import { UnclaimedDomainResponse } from './types';

/** @internal */
export type ResolutionServiceMap = {
  [key in NamingServiceName]: EthereumNamingService;
};

/** @internal */
export type ResolutionService = EthereumNamingService | Udapi;

/**
 * Blockchain domain Resolution library - Resolution.
 * Provides a way to resolve a domain name using various naming services
 * @example
 * ```
 * let resolution = new Resolution();
 * let result = await resolution.address('resolver.eth', 'ETH');
 * ```
 */
export default class Resolution {
  readonly blockchain: boolean;
  readonly serviceName: NamingServiceName;
  private readonly services: ResolutionServiceMap;

  /**
   * Creates a naming service instance
   * @param source - main configuration object
   * @param source.blockchain - blockchain configuration object
   * @param source.blockchain.ens - ens configuration object
   * @param source.blockchain.ens.url - blockchain api url
   * @param source.blockchain.ens.registryAddress - address of ens registry contract
   * @param source.blockchain.cns - cns configuration object
   * @param source.blockchain.cns.url - blockchain api url
   * @param source.blockchain.cns.registryAddress - address of cns registry contract
   * @param source.api - resolution api configuration object
   * @param source.api.url - resolution api url
   */
  constructor({
    blockchain = true,
    api = DefaultAPI,
    ...blockchainSource
  }: {
    blockchain?: boolean | SourceDefinition;
    api?: SourceDefinition;
  }) {
    this.blockchain = !!blockchain;
    this.serviceName = this.getServiceName();
    if (this.serviceName !== 'UDAPI') {
      const web3Provider = this.web3Provider(blockchainSource);
      this.services = {
        [NamingServiceName.CNS]: new Cns(web3Provider),
        [NamingServiceName.ENS]: new Ens(web3Provider),
        [NamingServiceName.ZNS]: new Zns(),
      };
    }
    if (!this.blockchain) {
      this.services = {
        [NamingServiceName.UDAPI]: new Udapi(api),
      };
    }
  }

  /**
   * Resolves domain name to a specific cryptoAddress
   * @async
   *
   * @param domain - domain name to be resolved
   * @param currencyTicker - currency ticker like BTC, ETH, ZIL, etc.
   * @returns A promise that resolves in a string
   */
  async address(domain: string, currencyTicker: string): Promise<string> {
    const data = await this.addressOrThrow(domain, currencyTicker);
    return data.address;
  }

  /**
   * Resolves domain name to a specific cryptoAddress or throws an error if not found or not supported by network.
   *
   * @async
   *
   * @param domain - domain name to be resolved
   * @param currencyTicker - currency ticker like BTC, ETH, ZIL, etc.
   */
  async addressOrThrow(domain: string, currencyTicker: string): Promise<{ address: string; coin: number }> {
    const method = this.isSupportedDomain(domain) ? 'addr' : 'address';
    const data = await this.resolver(domain)[method](domain, currencyTicker);
    if (!data)
      throw new ResolutionError(ResolutionErrorCode.UnspecifiedCurrency, {
        domain,
        currencyTicker,
      });
    return data;
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
