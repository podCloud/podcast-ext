# Podcast RSS extension

This project aims to extend the RSS XML to add metadatas about the show and its episodes

The podcast-ext project is open source and open to everyone wanting to contribute. 

You can start to share your ideas by opening Github issues at : 
https://github.com/podcloud/podcast-ext/issues

## Namespace
The `podext` namespace will be used to be fully platform agnostic and neutral.

## Podcast links

A new set of tags will permit podcasters to add social and podcasting platforms informations

- `podext:platform` adds informations about where to find the podcast on podcast platforms (iTunes link, Spotify link, etc)
- `podext:social` adds urls to any social network related to the podcast
- `podext:donate` adds urls to a donation platform
- `podext:shop` adds urls to a shop
- `podext:link` can be used to add any other link related to the podcast

## License
    
- `podext:license` tag should contain any license for the podcast (Creative Commons, private license, etc)

You can add this tag at channel level and item level.

## Platform blocks

The feed owner can choose specificaly which podcasting platform is allowed or not to add the podcast to their catalog :
`<podext:block platform="PLATFORM_NAME">yes/no</podext:block>`

A `default` platform name can be used to define the default behaviour an unlisted podcasting platform should adopt.

This mimicks `itunes:block` and `googleplay:block` mechanism, but aims to be platform independant, and generic, to be able
to add a new platform setting without the platform needing to extends rss on itself.

You can add this tag at channel level and item level.

## Team and Guests

You can credit the people behind the podcast or an episode by using the `podext:team` tag.
Childrens of `podext:team` tag can have a `role` attribute. (host, columnist, etc)

If you had guest on an episode, you can add them to the `podext:guests` tag.

Both tags is a list of `podext:person` tags

## Persons

A `podext:person` tag can be used in `podext:team` and `podext:guest` lists. 
This `podext:person` tag can have childrens to add informations about their social networks or websites: 
    `podext:social`, `podext:link`

This tag can also be used as a standalone tag on episodes metadata tags

## Episode metadata tags

Any episodes can contains an infinite amount of tags to provide more data about the content of the episode.
This include `podext:person` if the episode is talking about a person (and said person is not a guest of the episode).

This also include the following tags (with some attributes examples) : 

- `podext:book` with attributes `isbn`, `title`, `author`, `href` (link to the book on any website)
- `podext:game` with attributes `title`, `developer`, `publisher`, `platforms`, `href`
- `podext:tv_show` with attributes `title`, etc
- `podext:movie`
- `podext:music`
- `podext:art`
- `podext:object` (any object, a car, a computer, a furniture, a puree press etc..)
- `podext:location` with `name`, `lat`, `lng`, `address`, `city`, `postcode`, `country`
- `podext:website` for any website
- `podext:event` with `name` and `at` attributes, and with some childrens : `podext:location`, `podext:website`
- `podext:podcast` to add informations about any other podcast. Can use some childrens used at channel level : `podext:platform`, `podext:social` etc.

## Status

This is a work in progress, a first draft of the idea is available below, and the first XSD spec is at conception stage.

## Contributions

Anyone, and any podcasting platform can contribute. This work aims to make podcast datas better for the common good. 
Issues and pull requests are open.

## Example (first draft)

```xml
<rss version="2.0" xmlns:podext="https://podcast-ext.org">
	<channel>
		<!-- [...] -->

		<podext:platform platform="itunes" href="https://podcast.apple.com/mypodcast" />
		<podext:social platform="twitter" handle="pofmagicfingers" href="https://twitter.com/pofmagicfingers" />
		<podext:social platform="facebook" handle="pofmagicfingers" href="https://facebook.com/pofmagicfingers" />
		<podext:donate platform="patreon" handle="pofmagicfingers" href="https://patreon.com/pofmagicfingers" />
		<podext:shop platform="spreadshirt" href="https://spreadshirt.com/pofmagicfingers">Buy our stuff!</podext:shop>
		<podext:link href="https://podcloud.app/user/pofmagicfingers">My podCloud profile</podext:link>

		<podext:block platform="itunes">yes</podext:block>
		<podext:block platform="majelan">yes</podext:block>
		<podext:block platform="googleplay">no</podext:block>
		<podext:block platform="spotify">no</podext:block>
		<podext:block platform="podcloud">yes</podext:block>

		<podext:team>
			<podext:person firstname="André" lastname="Michot" nickname="Michan" role="host" pronoun="they" />
		</podext:team>

		<item>
			<!-- [...] -->
			<podext:book isbn="1241234432" title="ABC" author="Michel" href="https://amazon.co.uk/azeaze" />
			<podext:game title="ABC" developer="Blizzard" publisher="Activision" />
			<podext:tv_show title="Stranger things" />
			<podext:movie title="ABC" director="André" />
			<podext:video title="ABC" href="https://vimeo.com/video/1234123" />
			<podext:music title="ABC" artist="Jackson5" href="https://music.com/abc" />
			<podext:art title="ABC" artist="Jackson5" href="https://music.com/abc" />
			<podext:object name="Model S" brand="Tesla" price="82500" currency="EUR" href="https://www.tesla.com/fr_FR/models" />
			<podext:person firstname="André" lastname="Michot" nickname="Michan" />
			<podext:person firstname="Michel" lastname="Maurice" nickname="Mimau">
				<podext:social platform="twitter" handle="mimau" />
			</podext:person>

			<podext:team>
				<podext:person firstname="André" lastname="Michot" nickname="Michan" role="host" />
				<podext:person firstname="Alexis" lastname="Blablo" nickname="blablo" role="columnist" />
			</podext:team>

			<podext:guests>
				<podext:person firstname="Thomas" lastname="Collins">
					<podext:link href="https://jaimelegif.com">Thomas project website</podext:link>
          <podext:social platform="twitter" handle="tomcol" href="https://twitter.com/tomcol" />
				</podext:person>
			</podext:guests>

			<podext:location name="ABC" city="London" postcode="123VE" country="UK" lat="34.676637" lng="135.506512" />
			<podext:website name="Netflix" href="https://netflix.com" />
			<podext:event 

				name="MP3@Paris" 
				when="Sat, 22 June 2019 10:00:00 CEST" 
				where="Campus Jussieu" 
				lat="48.847520"
				lng="2.354047" 
				href="https://mp3aparis.fr" />
			<podext:podcast name="P2P" href="https://p2p.lepodcast.fr" rss="https://p2p.lepodcast.fr/rss" />
			<podext:podcast name="P2P" href="https://p2p.lepodcast.fr" rss="https://p2p.lepodcast.fr/rss">
				<podext:platform platform="spotify" href="https://open.spotify.com/sdfsdf" />
			</podext:podcast>
		</item>
	</channel>
</rss>
```
