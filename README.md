# Solana Blog

Welcome to the **Solana Blog** project repository! This decentralized application (DApp) leverages blockchain technology to showcase your ideas using this platform on the Solana network. Here you can write blogs and tell your story to the world. This project is built using Solana and Anchor.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Smart Contracts](#smart-contracts)
- [Testing](#testing)
- [Frontend](#frontend)
- [Contributing](#contributing)

## Overview

The **Solana Blog** provides a user to share there thoughts and ideas to the world. The user can write blogs and publish them on the blockchain. The user can also read blogs written by other users. In future we can add this functionality that the user can also tip the author of the blog if they like the blog, the user can also comment on the blog and interact with other users.

## Features

- **Write Blogs**: The user can write blogs and publish them on the blockchain.
- **Read Blogs**: The user can read blogs written by other users.
- **Tip the Author**: The user can tip the author of the blog if they like the blog.
- **Comment on Blogs**: The user can comment on the blog and interact with other users.
- **Solana Blockchain**: The project is built on the Solana blockchain.
- **Anchor**: The project is built using Anchor.


## Getting Started

Follow these steps to set up the project locally.

### Prerequisites

1. Node.js: Ensure Node.js is installed. Download it from [nodejs.org](https://nodejs.org/).
2. Anchor: Ensure Anchor is installed. Follow the instructions [here](https://www.anchor-lang.com/docs/installation).

### Installation

1. Clone the repository:

```bash
  git clone https://github.com/AbhimanyuAjudiya/solana-blog
```

2. Navigate to the project directory:

```bash
  cd solana-blog
```

3. Install required npm packages:

```bash
 npm install
```
## Usage

1. Build your project:

```bash
 anchor build
```

2. Make sure that your program ID is updated and run:
    
```bash
 anchor test
```

3. Now run the frontend:

```bash
 yarm dev
```

4. Open your web browser and navigate to `http://localhost:3000` to access the DApp.

5. Connect your wallet (e.g., Phantom) to the DApp.

6. Write your blog and publish it on the blockchain. You can also read blogs written by other users.

## Smart Contracts

This smart contract essentially manages a blogging system on the Solana blockchain. Users can create accounts, sign up, and create posts, with each post linked to the previous one. The contract also emits events to track the creation of posts. Users interact with this contract through Solana's blockchain tools and SDKs.

## Testing

You can test the smart contract using [solana playground](https://beta.solpg.io/) smart contract testing tool. 
Here is the code for the smart contract:

```rust
use anchor_lang::prelude::*;
use anchor_lang::solana_program::entrypoint::ProgramResult;

declare_id!("vETvRLApSDos1P1mherqU1HCiBskkLcrdE6KcZ8K4ix");

#[program]
pub mod blog_sol {

    use super::*;

    pub fn init_blog(ctx: Context<InitBlog>) -> ProgramResult {
        let blog_account = &mut ctx.accounts.blog_account;
        let genesis_post_account = &mut ctx.accounts.genesis_post_account;
        let authority = &mut ctx.accounts.authority;

        blog_account.authority = authority.key();
        blog_account.current_post_key = genesis_post_account.key();

        Ok(())
    }

    pub fn signup_user(ctx: Context<SignupUser>, name: String, avatar: String) -> ProgramResult {
        let user_account = &mut ctx.accounts.user_account;
        let authority = &mut ctx.accounts.authority;

        user_account.name = name;
        user_account.avatar = avatar;
        user_account.authority = authority.key();

        Ok(())
    }

    pub fn create_post(ctx: Context<CreatePost>, title: String, content: String) -> ProgramResult {
        let blog_account = &mut ctx.accounts.blog_account;
        let post_account = &mut ctx.accounts.post_account;
        let user_account = &mut ctx.accounts.user_account;
        let authority = &mut ctx.accounts.authority;

        post_account.title = title;
        post_account.content = content;
        post_account.user = user_account.key();
        post_account.authority = authority.key();
        post_account.pre_post_key = blog_account.current_post_key;

        blog_account.current_post_key = post_account.key();

        emit!(PostEvent {
            label: "CREATE".to_string(),
            post_id: post_account.key(),
            next_post_id: None
        });

        Ok(())
    }

  

   
}

#[derive(Accounts)]
pub struct InitBlog<'info> {
    #[account(init, payer = authority, space = 8 + 32 + 32 + 32 + 32)]
    pub blog_account: Account<'info, BlogState>,
    #[account(init, payer = authority, space = 8 + 32 + 32 + 32 + 32 + 8)]
    pub genesis_post_account: Account<'info, PostState>,
    #[account(mut)]
    pub authority: Signer<'info>,
    pub system_program: Program<'info, System>,
}

#[derive(Accounts)]
pub struct CreatePost<'info> {
    #[account(init, payer = authority, space = 8 + 50 + 500 + 32 + 32 + 32 + 32 + 32 + 32)]
    pub post_account: Account<'info, PostState>,
    #[account(mut, has_one = authority)]
    pub user_account: Account<'info, UserState>,
    #[account(mut)]
    pub blog_account: Account<'info, BlogState>,
    #[account(mut)]
    pub authority: Signer<'info>,
    pub system_program: Program<'info, System>,
}



#[derive(Accounts)]
pub struct SignupUser<'info> {
    #[account(init, payer = authority, space = 8 + 40 + 120  + 32)]
    pub user_account: Account<'info, UserState>,
    #[account(mut)]
    pub authority: Signer<'info>,
    pub system_program: Program<'info, System>,
}

#[event]
pub struct PostEvent {
    pub label: String,
    pub post_id: Pubkey,
    pub next_post_id: Option<Pubkey>,
}

#[account]
pub struct BlogState {
    pub current_post_key: Pubkey,
    pub authority: Pubkey,
}

#[account]
pub struct UserState {
    pub name: String,
    pub avatar: String,
    pub authority: Pubkey,
}

#[account]
pub struct PostState {
    title: String,
    content: String,
    user: Pubkey,
    pub pre_post_key: Pubkey,
    pub authority: Pubkey,
}
```

--Or

Smart contract tests are located in the `test` folder. These tests ensure the correct functioning of the smart contract. To run the tests, follow these steps:

1. Open a terminal in the project directory.
2. Run the following command to execute the tests:

```bash
 anchor build
 anchor test
```

This command will initiate the smart contract tests and display the results in the terminal.

## Frontend

The frontend of this DApp is built using React.js. It allows users to interact with the application and perform various actions. The frontend is located in the `app` folder.

- **React.js**: Powers the DApp's user interface.
- **Phantom**: A popular wallet browser extension for secure transactions.

## Contributing

Contributions to this project are welcome! To contribute:

1. Fork the repository.
2. Create a new branch for your feature/bug fix.
3. Make changes and test thoroughly.
4. Commit with clear and concise messages.
5. Push changes to your fork.
6. Submit a pull request describing your changes.
