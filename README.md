# icreact create a React based project and host it on the IC.


You want to create a React project and host it on the IC. 

There are 2 ways to it.

1. Convert the dfx generated asset web project into react project 
OR 
2. use https://create-react-app.dev/ to create React project and them embedd it into the asset canister.


This example explores the latter i.e creating a React project from https://create-react-app.dev/ and embedding it into the dfx project.


## Steps



1. Create a dfx project with no frontend. This won't create any npm or webpack bootstrapping for your web contents. 
All you will have is 2 canisters, a rust canister 'icreact' and assset canister 'icreact_asset'.

```bash
dfx new --no-frontend --type=rust icreact
```

2. Create a vanilla react project using create-react-app helper
```bash
cd icreact
npx create-react-app my-app
```
This will create react app in the my_app folder.

3. Change the source of the asset canister to point to the my-app build output in dfx.json.

```bash
  "finalcro_assets": {
      "type": "assets",
      "frontend": {
+	  "entrypoint": "my-app/build/index.html"
      },
      "source": [
-         "dist"
+         "my-app/build"
      ],
      "dependencies": [
        "finalcro"
      ]
    }
```

4. Build the my_app react project

```bash
   cd icreact/my-app
   npm run build
```

5. Deploy the canister
```bash
cd icreact
dfx create canister --all
dfx build 
dfx deploy
```



-------

Welcome to your new icreact project and to the internet computer development community. By default, creating a new project adds this README and some template files to your project directory. You can edit these template files to customize your project and to include your own code to speed up the development cycle.

To get started, you might want to explore the project directory structure and the default configuration file. Working with this project in your development environment will not affect any production deployment or identity tokens.

To learn more before you start working with icreact, see the following documentation available online:

- [Quick Start](https://smartcontracts.org/docs/quickstart/quickstart-intro.html)
- [SDK Developer Tools](https://smartcontracts.org/docs/developers-guide/sdk-guide.html)
- [Rust Canister Devlopment Guide](https://smartcontracts.org/docs/rust-guide/rust-intro.html)
- [ic-cdk](https://docs.rs/ic-cdk)
- [ic-cdk-macros](https://docs.rs/ic-cdk-macros)
- [Candid Introduction](https://smartcontracts.org/docs/candid-guide/candid-intro.html)
- [JavaScript API Reference](https://erxue-5aaaa-aaaab-qaagq-cai.raw.ic0.app)

If you want to start working on your project right away, you might want to try the following commands:

```bash
cd icreact/
dfx help
dfx config --help
```

## Running the project locally

If you want to test your project locally, you can use the following commands:

```bash
# Starts the replica, running in the background
dfx start --background

# Deploys your canisters to the replica and generates your candid interface
dfx deploy
```

Once the job completes, your application will be available at `http://localhost:8000?canisterId={asset_canister_id}`.


 

