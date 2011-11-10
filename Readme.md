# Hermes: A Mercury CMS #

## Development Notes ##

So, this is a proof of concept for a CMS using the Mercury HTML5 Editor.  First try will be to use Sinatra+DataMapper to keep it simple.  If that fails, then we will use Rails. 

### Rev 1 ###

- Public Editing
- Public Page Creation

When you go to a URL, the app will use a wildcard route to catch the request.  It will do a search of the Mercury data to see if there is page data available.  If so, it renders the data.  If not, then it puts up a blank html page with a form that lets the user specify the Title of a new page.  The title targets the only other Sinatra controller action, it creates a new, empty Mercury page entry, then just refreshes the current URI.

Note: Let's make it fun, you can use *whatever URI you want that aren't used by mercury*.  That means if you want to create a URI like: `host.com/info.php?this-is-my_page-man&yeah&no=3`, then that is totally allowed.

To reasonably hide the Mercury URIs, we should stick them someplace out of the way, like `host.com/__mercury/*`.  Hermes specific stuff can go into `__hermes`.

Should we refuse any generated URIs that have `/^__.*$/`?  Maybe.

### Rev 2 ###

- User Management

 - `__hermes/login`: log into the app. All users are admins.  
 - `__hermes/users`: user CRUD (RESTful)

All users are admins, but you can't edit unless you are logged in.  Also, require a session for the POST actions of Mercury.

### Rev 3 ###

- Templates

We will not always want to be able to edit the entire page, nor will we want to have to go to every page and commit the same edits to static site elements like headers, footers, menus, etc.  We should provide an interface for a user to specify certain page elements for editability, and also for site-wide consistency (through html classes, for instance)s