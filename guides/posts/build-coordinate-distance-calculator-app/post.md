---
title: How to build a Coordinate Distance Calculator App using Distance Calculator API?
description: "In this piece, let's build an app together that will show us the distance between two geographical coordinatesz."
publishedDate: 2022-01-31T07:18:41.708Z
lastModifiedDate: 2022-01-31T07:18:41.708Z
authors:
    - saad
categories:
    - apps
tags:
    - rapidapi
    - coordiante-distance-calculate-app
coverImage: ''
---

<Lead>

There are thousands of APIs available on [RapidAPI Hub](https://RapidAPI.com/hub?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel) that you can use to build different applications. Today, I will use one of these APIs to develop a coordinate distance calculator web app. So without any further ado, let’s jump in!

</Lead>

## Stack

We need to choose a stack first to build this application. I have decided to go with the [Jamstack](https://jamstack.org/).

I am going to use [Next.js](https://nextjs.org/) for the frontend and [TailwindCSS](https://tailwindcss.com/) for the styling.

If you don’t know about Next.js, it is a JavaScript framework built on top of React and provides features like server-side rendering, static site generation, etc. Tailwind is a CSS framework that provides utility classes to speed up the development process.

## Choosing The API

Let’s find an API that we can use to find the distance between coordinates. Go to [RapidAPI Hub](https://RapidAPI.com/hub?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel) and [create an account](https://RapidAPI.com/auth/sign-up?referral=/hub?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel) if you haven’t already and then search for “coordinates distance” in the search section.

<Callout
	title="Deep dive"
	linkText="Read more"
	linkHref="https://rapidapi.com/learn/hub"
>
	Learn more about how to use RapidAPI Hub.
</Callout>

You will see different search results related to coordinates distance API. For this piece, I am using [Distance Calculator API](https://RapidAPI.com/ApiOcean/api/distance-calculator?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel).

To use this API, you need to subscribe to it first. You can do this by clicking on **Subscribe to Test** button.

![Subscribe to Distance Calculator API](https://raw.githubusercontent.com/RapidAPI/DevRel-Stack-Data/7ef1b6ce2ca6e5796e89b6d18167f8b8ebb70e7e/guides/posts/build-coordinate-distance-calculator-app/images/subscribe.png)

Once you click the button, you will be redirected to another page where different available subscription packages will be shown. Let’s go with the free one for now.

After all this, you will be redirected back to the original page. Here you will have a key `x-rapidapi-key`. Save it. It will be used later in the application.

## Building The UI

You can create a Next.js boilerplate with TailwindCSS integrated by running the following command in your terminal. So let’s do that.

```sh
npx create-next-app -e with-tailwindcss coordinate-distance-calculator-app
```

This command is going to take a minute to set everything up. After generating the boilerplate, you will see a folder with the name `coordinate-distance-calculator-app` has been created. Open this folder in your preferred code editor. I will use [VSCode](https://code.visualstudio.com/) for this project.

### Project Files

When you open the project in your code editor, you will see the following directories and files in the root directory:

-   `pages` directory: Inside it, you will have files `index.js`, `_app.js`, and another directory called - - `api`. You only need to know about the `index.js` file that is the main entry point in your project.
-   `public` directory: This directory contains icons. You place your static files here to load later in the application.
-   `node_modules`: It’s another directory that contains all the node modules you are using in your application.
-   `package.json`: This file contains the metadata of your project.
-   `package-lock.json`: This file is responsible for tracking the exact version of every installed package.
-   `postcss.config.js`: This file contains [PostCSS](https://github.com/postcss/postcss) configurations.
-   `tailwind.config.js`: It contains [TailwindCSS](https://tailwindcss.com/) configurations.
-   `readme.md`: It’s a markdown file for documentation.

Before we move on to writing the code, open [this](https://github.com/RapidAPI/DevRel-Examples-External/blob/main/coordinate-distance-calculator-app/tailwind.config.js) file, and copy all of its content, then paste it inside the `tailwind.config.js` file in your project. These are some TailwindCSS configurations I have done specifically for this project. I have added some colors that you do not have by default with TailwindCSS and set some screen sizes.

Now let’s start writing the code. I am going to do it in steps so you can follow along:

```jsx
export default function Home() {
	return (
		<div className="flex flex-col items-center relative min-h-screen">
			<h2 className="font-raleway font-bold text-center text-6xl text-primary pt-20 pb-6 md:text-3xl">
				Coordinate <span className="text-secondary">Distance</span>{' '}
				Calculator App
			</h2>
			<h3 className="text-lightGrey text-2xl font-raleway font-bold uppercase tracking-wide mb-12 md:text-base md:px-4 md:text-center">
				Calculate the distance between two coordinates
			</h3>
		</div>
	);
}
```

It will create two headings for you with the text “Coordinate Distance Calculator App” and “Calculate the distance between two coordinates”. You can change it to anything you prefer.

### → STEP #2

Now let’s create two input fields and a calculate button. The user will be able to type the two coordinate sets in the input boxes and use the calculate button to get the distance between the coordinates.

For this, copy the following code and paste it in `pages/index.js`:

```jsx
export default function Home() {
	return (
		<div className="flex flex-col items-center relative min-h-screen">
			<h2 className="font-raleway font-bold text-center text-6xl text-primary pt-20 pb-6 md:text-3xl">
				Coordinate <span className="text-secondary">Distance</span>{' '}
				Calculator App
			</h2>
			<h3 className="text-lightGrey text-2xl font-raleway font-bold uppercase tracking-wide mb-12 md:text-base md:px-4 md:text-center">
				Calculate the distance between two coordinates
			</h3>
			<div className="flex flex-col justify-between items-center w-full md:items-center">
				<form className="flex w-full justify-center md:flex-col md:w-5/6">
					<input
						autoFocus={true}
						className="border-none outline-none bg-primary px-4 py-2 w-1/6 mx-2 rounded-sm font-raleway md:w-full md:mx-0"
						placeholder="Enter first coordinate set..."
					/>
					<input
						className="border-none outline-none bg-primary px-4 py-2 w-1/6 mx-2 rounded-sm font-raleway md:w-full md:mx-0"
						placeholder="Enter second coordinate set..."
					/>
					<button className="outline-none border border-danger font-bold font-raleway ml-4 px-12 py-2 rounded-sm bg-danger text-primary transition duration-300 hover:bg-bc hover:text-black md:ml-0 md:mt-4">
						Calculate
					</button>
				</form>
			</div>
		</div>
	);
}
```

This code is going to create two input fields and a button. I have also styled them a little bit using [TailwindCSS](<(https://tailwindcss.com/)>).

### → STEP #3

Let’s create some states to store the coordinate sets and the distance between coordinates that we will receive from the API. For this, copy-paste the following code in `pages/index.js`:

```jsx
import {useState} from 'react';

export default function Home() {
	const [firstCoordinateSet, setFirstCoordinateSet] = useState('');
	const [secondCoordinateSet, setSecondCoordinateSet] = useState('');
	const [res, setRes] = useState('');

	return (
		<div className="flex flex-col items-center relative min-h-screen">
			<h2 className="font-raleway font-bold text-center text-6xl text-primary pt-20 pb-6 md:text-3xl">
				Coordinate <span className="text-secondary">Distance</span>{' '}
				Calculator App
			</h2>
			<h3 className="text-lightGrey text-2xl font-raleway font-bold uppercase tracking-wide mb-12 md:text-base md:px-4 md:text-center">
				Calculate the distance between two coordinates
			</h3>
			<div className="flex flex-col justify-between items-center w-full md:items-center">
				<form className="flex w-full justify-center md:flex-col md:w-5/6">
					<input
						autoFocus={true}
						className="border-none outline-none bg-primary px-4 py-2 w-1/6 mx-2 rounded-sm font-raleway md:w-full md:mx-0"
						placeholder="Enter first coordinate set..."
						onChange={e => setFirstCoordinateSet(e.target.value)}
					/>
					<input
						className="border-none outline-none bg-primary px-4 py-2 w-1/6 mx-2 rounded-sm font-raleway md:w-full md:mx-0"
						placeholder="Enter second coordinate set..."
						onChange={e => setSecondCoordinateSet(e.target.value)}
					/>
					<button className="outline-none border border-danger font-bold font-raleway ml-4 px-12 py-2 rounded-sm bg-danger text-primary transition duration-300 hover:bg-bc hover:text-black md:ml-0 md:mt-4">
						Calculate
					</button>
				</form>
			</div>
		</div>
	);
}
```

You can see that I have added an `onChange` event handler to set the state value as soon as the user types something in the input box.

### → STEP #4

Let’s integrate the API now. For this, first, create a `.env.local` file and paste the following in it:

```sh
NEXT_PUBLIC_RAPIDAPI_KEY=YOUR-RAPIDAPI-KEY
```

You need to replace `YOUR-RAPIDAPI-KEY` here with the API key you got when you subscribed to the [Distance Calculator API](https://RapidAPI.com/ApiOcean/api/distance-calculator?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel). It is the value of `x-rapidapi-key` that you saved earlier.

Now download and add `axios` in your project. For this, run the following command in the terminal:

```sh
npm install axios
```

Now import `axios` at the top of the `pages/index.js`.

```js
import axios from ‘axios’;
```

### → STEP #5

RapidAPI Hub provides you with code snippets in different languages for integrating the API. I am going to use the `(JavaScript) Axios` one.

![Fetching data using (JavaScript) Axios](https://raw.githubusercontent.com/RapidAPI/DevRel-Stack-Data/7ef1b6ce2ca6e5796e89b6d18167f8b8ebb70e7e/guides/posts/build-coordinate-distance-calculator-app/images/code-snippet.png)

Now create a file with the name `calculate.js` inside the `pages/api` directory. It is going to create a REST API endpoint for you. The endpoint point will look like this:

```sh
http://localhost:3000/api/calculate
```

Now copy the following code in this file:

```js
import axios from 'axios';

export default function handler(req, res) {
	if (req.method === 'GET') {
		const options = {
			method: 'GET',
			url: 'https://distance-calculator.p.rapidapi.com/v1/one_to_one',
			params: {
				start_point: req.query.firstCoordinateSet,
				end_point: req.query.secondCoordinateSet,
				unit: 'miles',
				decimal_places: '2'
			},
			headers: {
				'content-type': 'application/json',
				'x-rapidapi-host': 'distance-calculator.p.rapidapi.com',
				'x-rapidapi-key': process.env.NEXT_PUBLIC_RAPIDAPI_KEY
			}
		};

		axios
			.request(options)
			.then(function (response) {
				res.status(200).json(response.data);
			})
			.catch(function (error) {
				console.error(error);
			});
	} else {
		res.status(400);
	}
}
```

This code makes an API call to the [Distance Calculator API](https://RapidAPI.com/ApiOcean/api/distance-calculator?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel) on the server and returns the results to the user. It executes when the user makes an API call to the `calculate` endpoint I mentioned above.

Once you are done, copy the following code in the `pages/index.js` file:

```jsx
import {useState} from 'react';
import axios from 'axios';

export default function Home() {
	const [firstCoordinateSet, setFirstCoordinateSet] = useState('');
	const [secondCoordinateSet, setSecondCoordinateSet] = useState('');
	const [res, setRes] = useState('');
	const [btnText, setBtnText] = useState('Calculate');

	/**
	 *
	 *
	 *
	 */
	const fetchCoordinatesDistance = async e => {
		e.preventDefault();

		try {
			setBtnText('Calculating...');
			const res = await axios.get(`/api/calculator`, {
				params: {
					firstCoordinateSet,
					secondCoordinateSet
				}
			});
			setRes(res.data);
		} catch (err) {
			console.log(err);
		}
		setBtnText('Calculate');
	};

	return (
		<div className="flex flex-col items-center relative min-h-screen">
			<h2 className="font-raleway font-bold text-center text-6xl text-primary pt-20 pb-6 md:text-3xl">
				Coordinate <span className="text-secondary">Distance</span>{' '}
				Calculator App
			</h2>
			<h3 className="text-lightGrey text-2xl font-raleway font-bold uppercase tracking-wide mb-12 md:text-base md:px-4 md:text-center">
				Calculate the distance between two coordinates
			</h3>
			<div className="flex flex-col justify-between items-center w-full md:items-center">
				<form className="flex w-full justify-center md:flex-col md:w-5/6">
					<input
						autoFocus={true}
						className="border-none outline-none bg-primary px-4 py-2 w-1/6 mx-2 rounded-sm font-raleway md:w-full md:mx-0"
						placeholder="Enter first coordinate set..."
						onChange={e => setFirstCoordinateSet(e.target.value)}
					/>
					<input
						className="border-none outline-none bg-primary px-4 py-2 w-1/6 mx-2 rounded-sm font-raleway md:w-full md:mx-0"
						placeholder="Enter second coordinate set..."
						onChange={e => setSecondCoordinateSet(e.target.value)}
					/>
					<button
						className="outline-none border border-danger font-bold font-raleway ml-4 px-12 py-2 rounded-sm bg-danger text-primary transition duration-300 hover:bg-bc hover:text-black md:ml-0 md:mt-4"
						onClick={fetchCoordinatesDistance}
					>
						{btnText}
					</button>
				</form>
				{res && (
					<div className="flex flex-col mt-16 w-3/6 h-4/5 md:flex-col md:w-4/6 md:h-full md:mb-12 md:w-4/5">
						<p className="mb-12 border border-secondary text-primary font-raleway px-4 py-8 tracking-wide leading-8">
							The total distance between these two coordinates is{' '}
							{res.distance} Miles
						</p>
					</div>
				)}
			</div>
			<div className="flex flex-col mt-10 justify-end h-36 md:h-24">
				<p className="block mb-10 text-center text-secondary text-xs">
					Made by RapidAPI DevRel Team -{' '}
					<a
						className="hover:text-primary"
						href="https://github.com/RapidAPI/DevRel-Examples-External"
					>
						See more examples like this
					</a>
				</p>
			</div>
		</div>
	);
}
```

You can see that I have created a function, `fetchCoordinatesDistance`, to request the API. I have also created a UI that is conditionally rendering on the screen based on the `res` state variable value.

## Wrap Up

That’s it. We have successfully built a [Coordinate Distance Calculator App](https://rapidapi-example-coordinate-distance-calculator.vercel.app/) using [Distance Calculator API](https://RapidAPI.com/ApiOcean/api/distance-calculator?utm_source=RapidAPI.com/guides&utm_medium=DevRel&utm_campaign=DevRel). You can find the source code of this web app [here](https://github.com/RapidAPI/DevRel-Examples-External/blob/main/coordinate-distance-calculator-app).

In the end, it will look something like this:

![Coordinate Distance Calculator built with Next.js and Distance Calculator API](https://raw.githubusercontent.com/RapidAPI/DevRel-Stack-Data/7ef1b6ce2ca6e5796e89b6d18167f8b8ebb70e7e/guides/posts/build-coordinate-distance-calculator-app/images/cover.png)