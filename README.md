# hugo-website

This website is mantained with Hugo.

## Running locally
- Install the latest Hugo Extended from GitHub (https://github.com/gohugoio/hugo/releases)
- Clone this repository `git clone https://github.com/jr-santos98/my-website/`
- Enter the new directory `cd my-website`
- Update git submodules `git submodule update --init --recursive`
- Run the local server `hugo server -D`

## Remote server setup

To deploy the website, run the following script:

`./deploy.sh`

It runs Hugo, converting the site from Markdown to HTML and CSS.
It saves the content in the "public" folder.
The "public" folder is another repository, which the script automatically
pushes to, updating the website.
