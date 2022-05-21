# ICReact

Sample repository that creates a React web app and hosts it on the Internet Computer(IC).

Contents in this repository are the results of steps described in the README.md If
you are following the README.md to create a new project DON'T check out this repository.
Instead, just follow the steps outlined here.


## A note
There are 2 approaches for hosting a React web app in a dfx project
1. Embed a https://create-react-app.dev/ create react app in the dfx project.
Or
2. Convert the dfx generated web front-end into react project

This sample repository explores the former.

## Steps

1. Create a dfx project with no frontend.  This will skip the default webpack
and npm bootstrap code injected by `dfx new`.  Two canisters smart contracts are
created, a RUST canister 'icreact' and an asset canister 'icreact_asset'.  The
asset canister will not have any front end loaded into to. In the next steps, we
will load the react web app as an asset into this asset smart contract.

You can use either RUST or Motoko for your back-end canister --type=[rust|motoko].
```bash
dfx new --no-frontend --type=rust icreact
```

2. Create the vanilla react project using the create-react-app helper
Details can be founder here: https://create-react-app.dev
```bash
cd icreact
npx create-react-app my-app
```
This will create a self-contained react app in the my_app folder.

3. Build the my_app react project
```bash
   cd icreact/my-app
   npm run build
```

4. Modify the dfx.json to pick up the web asset from the react web app.
Apply the following patch to your dfx.json
```bash
# git diff ./dfx.json
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
Assets from my-app/build folder will be uploaded to your canister smart contract.
The `entrypoint` specifies the default asset to be returned for the `GET / HTTP` request.

5. Deploy the canister
```bash
cd icreact
dfx start --background
dfx canister create --all
dfx build
dfx deploy
```

6. Access your react app from the dfx deployed local IC network.

Deployed canisters.
URLs:
  Front-end:
    icreact_assets: http://127.0.0.1:8000/?canisterId=ryjl3-tyaaa-aaaaa-aaaba-cai


7. Live Rendering/Debugging

	You don't have to deploy your web app on the blockchain while developing.
	Debug/develop your react native app using the create-react-app
	tooling and then deploy the results on the blockchain.
