# Podcast RSS extension

This project aims to extend the RSS XML to add metadatas about the show and its episodes

The podcast-ext project will be open source and open to everyone wanting to contribute. 

You can share start to share your ideas by opening Github issues at : 
https://github.com/podcloud/podcast-ext/issues

## Namespace
    The `podcast` namespace will be used to be fully platform agnostic and neutral.

## Podcast links

    A new set of tags will permit podcasters to add social and podcasting platforms informations

    - `podcast:platform` adds informations about where to find the podcast on podcast platforms (iTunes link, Spotify link, etc)
    - `podcast:social` adds urls to any social network related to the podcast
    - `podcast:donate` adds urls to a donation platform
    - `podcast:shop` adds urls to a shop
    - `podcast:link` can be used to add any other link related to the podcast

## License
    
    - `podcast:license` tag should contain any license for the podcast (Creative Commons, private license, etc)

    You can add this tag at channel level and item level.

## Platform blocks
    
    The feed owner can choose specificaly which podcasting platform is allowed or not to add the podcast to their catalog :
    `<podcast:block platform="PLATFORM_NAME">yes/no</podcast:block>`
    
    A `default` platform name can be used to define the default behaviour an unlisted podcasting platform should adopt.

    This mimicks `itunes:block` and `googleplay:block` mechanism, but aims to be platform independant, and generic, to be able
    to add a new platform setting without the platform needing to extends rss on itself.

    You can add this tag at channel level and item level.

## Team and Guests

    You can credit the people behind the podcast or an episode by using the `podcast:team` tag.
    Childrens of `podcast:team` tag can have a `role` attribute. (host, columnist, etc)
    
    If you had guest on an episode, you can add them to the `podcast:guests` tag.

    Both tags is a list of `podcast:person` tags

## Persons

    A `podcast:person` tag can be used in `podcast:team` and `podcast:guest` lists. 
    This `podcast:person` tag can have childrens to add informations about their social networks or websites: 
        `podcast:social`, `podcast:link`

    This tag can also be used as a standalone tag on episodes metadata tags
    
## Episode metadata tags
    
    Any episodes can contains an infinite amount of tags to provide more data about the content of the episode.
    This include `podcast:person` if the episode is talking about a person (and said person is not a guest of the episode).

    This also include the following tags (with some attributes examples) : 

    - `podcast:book` with attributes `isbn`, `title`, `author`, `href` (link to the book on any website)
    - `podcast:game` with attributes `title`, `developer`, `publisher`, `platforms`, `href`
    - `podcast:tv_show` with attributes `title`, etc
    - `podcast:movie`
    - `podcast:music`
    - `podcast:art`
    - `podcast:object` (any object, a car, a computer, a furniture, a puree press etc..)
    - `podcast:location` with `name`, `lat`, `lng`, `address`, `city`, `postcode`, `country`
    - `podcast:website` for any website
    - `podcast:event` with `name` and `at` attributes, and with some childrens : `podcast:location`, `podcast:website`
    - `podcast:podcast` to add informations about any other podcast. Can use some childrens used at channel level : `podcast:platform`, `podcast:social` etc.

## Status

    This is a work in progress, a first draft of the idea is available below, and the first XSD spec is at conception stage.

## Contributions

    Anyone, and any podcasting platform can contribute. This work aims to make podcast datas better for the common good. 
    Issues and pull requests are open.

## Example (first draft)

```xml
<rss version="2.0" xmlns:podcast="https://podcast-ext.org">
	<channel>
		<!-- [...] -->

		<podcast:platform platform="itunes" href="https://podcast.apple.com/mypodcast" />
		<podcast:social platform="twitter" handle="pofmagicfingers" href="https://twitter.com/pofmagicfingers" />
		<podcast:social platform="facebook" handle="pofmagicfingers" href="https://facebook.com/pofmagicfingers" />
		<podcast:donate platform="patreon" handle="pofmagicfingers" href="https://patreon.com/pofmagicfingers" />
		<podcast:shop platform="spreadshirt" href="https://spreadshirt.com/pofmagicfingers">Buy our stuff!</podcast:shop>
		<podcast:link href="https://podcloud.app/user/pofmagicfingers">My podCloud profile</podcast:link>

		<podcast:block platform="itunes">yes</podcast:block>
		<podcast:block platform="majelan">yes</podcast:block>
		<podcast:block platform="googleplay">no</podcast:block>
		<podcast:block platform="spotify">no</podcast:block>
		<podcast:block platform="podcloud">yes</podcast:block>

		<podcast:team>
			<podcast:person firstname="André" lastname="Michot" nickname="Michan" role="host" pronoun="they" />
		</podcast:team>

		<item>
			<!-- [...] -->
			<podcast:book isbn="1241234432" title="ABC" author="Michel" href="https://amazon.co.uk/azeaze" />
			<podcast:game title="ABC" developer="Blizzard" publisher="Activision" />
			<podcast:tv_show title="Stranger things" />
			<podcast:movie title="ABC" director="André" />
			<podcast:video title="ABC" href="https://vimeo.com/video/1234123" />
			<podcast:music title="ABC" artist="Jackson5" href="https://music.com/abc" />
			<podcast:art title="ABC" artist="Jackson5" href="https://music.com/abc" />
			<podcast:object name="Model S" brand="Tesla" price="82500" currency="EUR" href="https://www.tesla.com/fr_FR/models" />
			<podcast:person firstname="André" lastname="Michot" nickname="Michan" />
			<podcast:person firstname="Michel" lastname="Maurice" nickname="Mimau">
				<podcast:social platform="twitter" handle="mimau" />
			</podcast:person>

			<podcast:team>
				<podcast:person firstname="André" lastname="Michot" nickname="Michan" role="host" />
				<podcast:person firstname="Alexis" lastname="Blablo" nickname="blablo" role="columnist" />
			</podcast:team>

			<podcast:guests>
				<podcast:person firstname="Thomas" lastname="Collins">
					<podcast:link href="https://jaimelegif.com">Thomas project website</podcast:link>
                    <podcast:social platform="twitter" handle="tomcol" href="https://twitter.com/tomcol" />
				</podcast:person>
			</podcast:guests>

			<podcast:location name="ABC" city="London" postcode="123VE" country="UK" lat="34.676637" lng="135.506512" />
			<podcast:website name="Netflix" href="https://netflix.com" />
			<podcast:event 
				name="MP3@Paris" 
				when="Sat, 22 June 2019 10:00:00 CEST" 
				where="Campus Jussieu" 
				lat="48.847520"
				lng="2.354047" 
				href="https://mp3aparis.fr" />
			<podcast:podcast name="P2P" href="https://p2p.lepodcast.fr" rss="https://p2p.lepodcast.fr/rss" />
			<podcast:podcast name="P2P" href="https://p2p.lepodcast.fr" rss="https://p2p.lepodcast.fr/rss">
				<podcast:platform platform="spotify" href="https://open.spotify.com/sdfsdf" />
			</podcast:podcast>
		</item>
	</channel>
</rss>
```
