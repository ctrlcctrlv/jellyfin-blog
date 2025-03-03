---
title: "Jellyfin Release - v10.8.0"
subtitle: "A new season dawns"
author: "Joshua Boniface & Shadowghost"
githubusername: "joshuaboniface Shadowghost"
date: 2022-06-10T20:00:00-04:00
justify: "center"
---

After a rather long development cycle the Jellyfin team is proud to announce stable version 10.8! This release post will mostly cover the highlights with little prose, as there is so much to cover!

<!--more-->

<a href="/downloads/" class="button button__accent">Download Jellyfin 10.8.0</a> <a href="https://github.com/jellyfin/jellyfin/releases/tag/v10.8.0" class="button hero__button">Read the full release notes</a>

All of the changes, accumulated over nearly the last two years, are too many to easily list, so we'll break them down in the sections below and hope all of you find something enjoyable.

The major highlighted changes are:

 *  numerous improvements to Hardware Acceleration (HWA), including:

     * Dolby Vision Profile 5 and 7 tone-mapping

     * CUDA-based tone-mapping for NVIDIA

     * extended OpenCL tone-mapping for Intel

     * hardware based subtitle burn in

     * Intel tone-mapping support for Windows

     * full OpenCL filtering for AMF on Windows

     * deprecation of OMX for raspberry pi, use V4L2 instead

 * proper network interface binding and handling of proxied requests

 * various fixes for DLNA, Sync-Play and m3u HTTP streams

 * DLNA disabled by default

 * extended NFO metadata import

 * external audio and subtitle support including container (mks, mka)

 * extended plain folder parsing

 * enhanced detection and handling of DVD/BD ISOs and folders

 * extend TMDb metadata provider (series state, season names, tags, logos, etc)

## Server
Some major fixes include a number of HWA improvements, explicit network interface binding, DLNA improvements, better NFO parsing, configuration cleanup (relics of the migrations in 10.7.z), and numerous metadata improvements, as well as the migration to .NET 6 which provides a nice stable language base for future improvements.

A point-form list of the changes compiled by the team is:

 *  General:

     * automatically migrate and cleanup config files

     * reduce memory footprint by various optimizations (e.g. reducing memory traffic)

     * rewrite QuickConnect

     * splashscreen in branding API (although not in use by any client yet)

     * various HDHomerun fixes and improvments

     * properly read filesize from symlinks

     * create output directory on file extraction

     * return path to pinfile on password reset

     * fix ombi auth through Jellyfin

     * include genre in related media generation

     * Implement more provider links for series, seasons, episodes and movies

     * properly handle gif

     * passwords are now hashed with 120000 iterations of PBKDF2-SHA512 instead of 1000 iterations of PBKDF2-SHA1, old passwords are migrated automatically on login

     * add config option to disable automatic server discovery

 * Networking:

     * fix explicit IP/interface binding

     * disable UPnP by default (only applies to new setups)

     * proper handling of published server URLs

     * disable DLNA server by default to avoid security risks

 * HWA:

     * implement CUDA-based tone-mapping for NVIDIA

     * extend Intel OpenCL tone-mapping (speed-wise on-par with VPP tone-mapping and therefore preferable)

     * implement full OpenCL HW filtering for AMD on Windows

     * implement hardware-based subtitle burn-in (significantly faster)

     * implement proper tone-mapping support on Windows

     * add CUDA & OpenCL tone-mapping support for Dolby Vision profile 5 and 8

     * various other fixes for NVIDIA and Intel hardware acceleration

     * add support for AV1 hardware decoding on supported platforms

     * deprecate Raspberry Pi OMX/MMAL hardware acceleration in favour of V4L2

 * Streaming/Transcoding:

     * optimize and extend DLNA support

     * fixes for DLNA PlayTo and DLNA folders

     * fixes for DLNA seeking

     * extraction of attached fonts for subtitle transcoding/burn-in

     * small fixes to SyncPlay

     * add transcoding information to playback data

     * fix opus sampling rates on transcode

     * properly stream m3u over HTTP

     * add keyframe extraction for better seeking (WARNING: this is a really long running task)

     * overhaul streaming logic to only transcode incompatible streams

     * various fmp4 fixes

 * NFO:

     * add parsing of additional ids

     * proper importing of watched state

     * proper parsing of ratings

     * proper handling of thumb tags

     * add support for fanart tag

     * proper casting of NFO ids to internal ids

 * Scanner/metadata providers:

     * add ID parsing from folder names

     * extend ID parsing from filenames

     * refactor extras parsing (way faster)

     * refactor and harden parsing of plain folders (all movies in one folder)

     * refactor and extend external subtitle and external audio parsing (now supports containers too)

     * properly handle unprobed strm playback with external streams

     * add support for TMDB absolute and TV order

     * properly pass language to TMDB search queries

     * fetch TMDB parental rating for tvshows

     * enable fetching additional series states from TMDb

     * properly detect DolbyVision

     * enhance detection and handling of DVD/BD folders/ISOs

     * episode parser improvements

     * add ability to disable adult content in TMDb

     * add ability to configure image scale in TMDb

     * update artist split whitelist

     * make tag import and maxCastMembers configurable for TMDb

     * improve metadata merging

     * add ability to fetch logos with TMDb

     * add option to configure season name importing for TMDb

 * Technical:

     * upgrade to latest .NET 6 (fixes some of the quirks with network storage)

     * bump all dependencies

     * upgrade analyzers and properly handle warnings

     * proper generation and publishing of OpenAPI spec

     * add and extend tests for various subsystems

     * upgrade Docker images to Debian 11 Bullseye

     * include latest Intel Compute Runtime in Docker images

     * add health check to Docker images

     * remove unused docker volume for /media from Docker images

     * make flushing to disk async if possible

## Web
Web has been moved completely to NPM (instead of Yarn), and several pages have been ported to React. Further many dozens of improvements and fixes have been made.

A point-form list of the changes compiled by the team is:

 * switch to NPM

 * update all dependencies

 * introduce ReactJS and migrate some pages

 * redesign of mobile item detail views

 * SyncPlay improvements

 * user settings for custom CSS

 * fixes for TV layouts

 * book player improvements and new Continue Reading section

 * change SyncPlay icon

 * add support for custom links in sidebar (config file only)

 * add support for new QuickConnect

 * update settings to reflect server changes

 * properly name generated bundles for cache-invalidation on update

 * implement markdown for plugin changelog rendering

 * add hardware transcoding info to playback data

 * enable buffering in the web player

 * switch volume slider to exponential instead of linear scaling

 * remove tag filter limit

 * fixes for theme songs and videos

 * unify duration display

 * add item count to playlists

 * expand metadata editor

 * various fixes for webOS

 * fix and extend multiselect

 * save playback speed between media

 * introduce WebWorker for blurhash decoding

 * update translations

 * add apple device icon to activity log

 * save pdf "playback" on page finish

 * stack toasts

 * add paging to list view

 * display series level extras on series page

 * extend LiveTV pages

 * extend mediainfo dialogue

 * escape most HTML

 * add rewatching to next up

 * allow markdown in login disclaimer

 * fix theme colors

 * tackle accessibility issues

 * fix album track sorting if audio files have SortName tags

 * add track sorting for videos

## FFmpeg
Our custom FFMpeg has been upgraded to version 5, along with numerous HWA enhancements and improvements.

A point-form list of the changes compiled by the team is:

 * update to FFmpeg 5.0.x

 * rename Debuntu package to jellyfin-ffmpeg5 for backwards compatibility

 * update existing patches

 * add patches for CUDA and Intel Quick Sync tone-mapping improvements

 * add patches for AMD Vulkan-based HWA and tone-mapping

 * add patches for CUDA & OpenCL tone-mapping support for Dolby Vision profiles 5 and 8

 * self-build and include latest Intel media-driver, required libraries and vainfo

 * migrate CI to Github Actions

 * add build script for win64

 * add required libs for QSV on 12th gen Intel hardware

 * add chromaprint

 * remove deprecated distros, add newly released distros

 * add patch to support long path names on Windows

## Plugins
All plugins have been updated for Jellyfin 10.8.0, as well as numerous day to day enhancements.

A point-form list of (some of) the changes compiled by the team is:

 * migrate CI to templated Github Action workflows

 * fix trakt.tv plugin to actually be useable

## Translations
Thanks to the many dozens of generous volunteers over at our Weblate (https://translate.jellyfin.org), thousands of new translations are available in Jellyfin 10.8.0 for over 3 dozen languages.

Happy watching!
