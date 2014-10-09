GitHub check-for-updates library
================================

Copyright (c) 2014 Pier Carlo Chiodi - http://www.pierky.com

Licensed under The MIT License (MIT) - http://opensource.org/licenses/MIT

https://github.com/pierky/githubchecknewrelease.js

Given the current version of a repository, this library checks for 
updated releases on GitHub. Data can be cached in order to perform
checks only at periodic intervals.

Requires:

	jQuery object, used for .ajax and .parseJSON

Usage:

	CheckNewRelease( {
		current_release: 'current_version',
		owner: 'repository_owner',
		repo: 'repository_name',

		done: function( Results ) {
		},

		// optional parameters
		instance: 'instance_id',
		include_pre_releases: true || false,
		check_interval: days,
		access_token: 'github_API_access_token',

		error: function( ErrorMessage ) {
		}
	} );

The current_release parameter must be set to the tag name of the
current release that identifies the version of the repository to
check updates for.

The instance parameter can be used to checks for multiple software 
on the same context. Cache data will be written locally using the 
instance tag to identify results.

The check_interval parameter is used to enable data caching.
It must be set with the number of days to wait between a check and
another. Cache works using browser's localStorage or cookie.

The access_token can be used to have a bigger rate-limit from GitHub.
Consider that rate-limit works on an IP address basis, so if used on
client-side applications it may be useless.

The 'done' callback function is executed to pass results to the caller.
It has one argument, Results:

	Results = {
		cached: true || false,
		new_release_found: true || false,

		// optional fields
		new_release: {
			version: 'version',
			name: 'name',
			published_at: 'date/time',
			prerelease: true || false,
			url: 'URL'
		},
		new_release_raw: <release object returned by GitHub API>
	}

- cached is set to true when no check has been performed and data is
returned from local cache;

- new_release is the object that describes the last release found on
GitHub; it's present only if new_release_found == true; version is 
the tag_name used on GitHub for the release.

