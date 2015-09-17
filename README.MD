# Devpost Expo / Table Number App

## What is it?

This is a [mobile-ready website](http://nealrs.github.io/expo/) for distributing and filtering table numbers at your hackathon expo. [Here's an example](http://nealrs.github.io/mhacks6/) from MHacks 6, where we had over 250 projects.

Everything is rendered client-side and the site is hosted on GitHub pages, so there's no backend / scaling issues to worry about. All you have to do is update the `data.csv` file and push it up to your `gh-pages` branch.

[You can read about the history of this project](http://devpost.com/software/hackathon-table-numbers) on Devpost.

## How to use this app

### Local setup

1. [Fork this repository](https://github.com/nealrs/expo#fork-destination-box) or  clone it to your local machine

  `git clone https://github.com/nealrs/expo.git`

2. Fire up a local webserver in your development directory (just for testing)

  `python -m SimpleHTTPServer`

  If you want to livereload changes, I suggest using [livereload](https://github.com/lepture/python-livereload). Otherwise you'll have to press refresh in your browser a lot (no big deal).

3. Go to [http://localhost:8000](http://localhost:8000) ( [localhost:35729](http://localhost:35729) if you're using livereload) to see the local app.

  It should look like this:

  ![](http://i.imgur.com/sf0FlXd.png)

### Adding your hackathon data

1. Open up `index.html` and locate the following code blocks:

  ```html
  <title>HackathonName Expo</title>

  <div class="container">
    <div id="header">
      <h1><a href="DevpostURL" title="HackathonName Expo"><img src="http://nealrs.github.io/devpost-follow-button/icon/devpost.svg" style="vertical-align:middle; width:60px;"> HackathonName</a><h1>
    </div>
    <div id="fullTable"></div>
  </div>
  ```

  - Change `HackathonName` to the name of your hackathon (e.g. PennApps XII)
  - Change `DevpostURL` to your hackathon's Devpost URL (e.g. http://mhacks6.devpost.com)
  - Add your own favicon & hackathon logo, we've put some placeholders in for now.

2. Open `data.csv` in **MS Excel or another spreadsheet app**

  ![](http://i.imgur.com/uDbPhe3.png)

    There are 5 columns in this sheet:
    - `expo` - Expo number (optional for large hackathons)
    - `table` - Table number
    - `project` - Project Name
    - `sponsors` - Applicable sponsor prizes
    - `link` - Link to project's Devpost page
    - `category` - Optional data field for additional filtering
    - `special`- Additional optional data field

    This is where you'll paste in submission data & assign table numbers. If you don't need the optional `category` or `special` columns, you can delete them from the spreadsheet, and also comment them out in the code as shown:

    ```html
    <table id="expoTable">
      <thead>
        <tr>
          <th class="number">Table</th>
          <th class="name">Project</th>
          <th class="prize">Sponsor Prizes</th>
          <!--<th class="cat">Category</th>-->
        </tr>
      </thead>
      <tbody class="list">
        {{#data}}
          <tr>
            <td class="number">E{{expo}} T{{table}}</td>
            <td class="name"><a href="{{{link}}}" target="_blank">{{project}}</a></td>
            <td class="prize">{{sponsors}}</td>
            <!--<td class="cat">{{category}}</td>-->
          </tr>
        {{/data}}
      </tbody>
    </table>
    ```

    I'd also recommend commenting out the `E{{expo}} ` tag unless you're running multiple expos.

3. Once the submission deadline is over, Go to the metrics tab on your hackathon dashboard and run a submissions export, _without_ PII.

    ![](http://i.imgur.com/8YIT03y.png)

    You'll receive a download link via email. Once you download the export, (it's a CSV) open it up in Excel and copy the following columns into their matching columns in `data.csv`:

    - `Submission Title` (A) -> `project` (C)
    - `Submission Url` (B) -> `link` (E)
    - `Sponsor Prizes` (usually G or H) -> `sponsors` (D)
    - Repeat for `category` or `special` if you're using them.

    Save your CSV!

4. Assign Expo & table numbers

    The app _does not_ automatically assign table / expo numbers. We leave that up to you. There's no one-size-fits-all solution, so you can use whatever system works for you. However, every row should have a unique combination of Expo & table numbers.

    Once you're done, go back to your browser and make sure everything is loads correctly.

    **NOTE** Using Excel or a spreadsheet app is crucial right now. Do _not_ edit `data.csv` with a text editor. Quinlan, I'm looking at you :unamused:)

    **ALSO** You must save this file as a CSV and commit+push it GitHub to update the list online.

5. Once you're satisfied, save everything, commit it, and push it up to your `gh-pages` branch.

  Your table numbers will be live at http://your_github_username.github.io/expo

### Custom URLs

If you have your own landing page / site for your hackathon, we suggest setting up a CNAME for a more user friendly URL. e.g. http://expo.funhacks.com. (It's a lot easier than http://derp78.github.com/hackathonname.)

If you need help setting up a CNAME, [read this](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/).

# Filters & sponsors

Finding specific hacks, filtering for keywords, and providing sponsors with their judging lists is SUPER EASY with the expo app.

1. You can use the search box to filter the entire table (all columns) based on any text string -- like hardware:

  ![](http://i.imgur.com/blRIYqK.png)

2. You can set the filter by using URL parameters

  Try this, add `?filter=SOME_API_NAME` to your url to create a unique, filtered list for each of your sponsors. For example, here's a list of hacks that mention Twilio:

  ![](http://i.imgur.com/OAh4bwU.png)

  Email them the link so they know exactly which tables to go to -- or take it a step further and print them a copy. The app contains custom print styles that save paper & ink.

  ![](http://i.imgur.com/ap9ITUW.png)

### Mobile browsing

We've included some 'sensible' mobile styles, which hide the category / special columns on small screens and collapse the borders. 

## Dasss it!
