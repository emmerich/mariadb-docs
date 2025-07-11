
# osmdb06.sql

Below is the schema described in the [OpenStreetMap Dataset Use](openstreetmap-dataset.md) article. To use, copy everything in the box below into a file called
'`osmdb06.sql`', then continue with the instructions.


```
-- phpMyAdmin SQL Dump
-- version 2.11.9.3
-- http://www.phpmyadmin.net
--
-- Хост: mysql.leonenko.info
-- Час стварэньня: 16 Сак 2009, 15:12
-- Вэрсія сэрвэра: 5.0.67
-- Вэрсія PHP: 5.2.6

SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;

--
-- База дадзеных: `osmapper_belarus`
--

-- --------------------------------------------------------

--
-- Структура табліцы `changesets`
--

DROP TABLE IF EXISTS `changesets`;
CREATE TABLE IF NOT EXISTS `changesets` (
  `id` bigint(20) NOT NULL auto_increment,
  `user_id` bigint(20) NOT NULL,
  `created_at` datetime NOT NULL,
  `min_lat` int(11) default NULL,
  `max_lat` int(11) default NULL,
  `min_lon` int(11) default NULL,
  `max_lon` int(11) default NULL,
  `closed_at` datetime NOT NULL,
  `num_changes` int(11) NOT NULL default '0',
  PRIMARY KEY  (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=20103 ;

-- --------------------------------------------------------

--
-- Структура табліцы `changeset_tags`
--

DROP TABLE IF EXISTS `changeset_tags`;
CREATE TABLE IF NOT EXISTS `changeset_tags` (
  `id` bigint(64) NOT NULL,
  `k` varchar(255) NOT NULL default '',
  `v` varchar(255) NOT NULL default '',
  KEY `changeset_tags_id_idx` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `current_nodes`
--

DROP TABLE IF EXISTS `current_nodes`;
CREATE TABLE IF NOT EXISTS `current_nodes` (
  `id` bigint(64) NOT NULL auto_increment,
  `latitude` int(11) NOT NULL,
  `longitude` int(11) NOT NULL,
  `changeset_id` bigint(20) NOT NULL,
  `visible` tinyint(1) NOT NULL,
  `timestamp` datetime NOT NULL,
  `tile` int(10) unsigned NOT NULL,
  `version` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `current_nodes_timestamp_idx` (`timestamp`),
  KEY `current_nodes_tile_idx` (`tile`),
  KEY `changeset_id` (`changeset_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=348816842 ;

-- --------------------------------------------------------

--
-- Структура табліцы `current_node_tags`
--

DROP TABLE IF EXISTS `current_node_tags`;
CREATE TABLE IF NOT EXISTS `current_node_tags` (
  `id` bigint(64) NOT NULL,
  `k` varchar(255) NOT NULL default '',
  `v` varchar(255) NOT NULL default '',
  PRIMARY KEY  (`id`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `current_relations`
--

DROP TABLE IF EXISTS `current_relations`;
CREATE TABLE IF NOT EXISTS `current_relations` (
  `id` bigint(64) NOT NULL auto_increment,
  `changeset_id` bigint(20) NOT NULL,
  `timestamp` datetime NOT NULL,
  `visible` tinyint(1) NOT NULL,
  `version` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `current_relations_timestamp_idx` (`timestamp`),
  KEY `changeset_id` (`changeset_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=80283 ;

-- --------------------------------------------------------

--
-- Структура табліцы `current_relation_members`
--

DROP TABLE IF EXISTS `current_relation_members`;
CREATE TABLE IF NOT EXISTS `current_relation_members` (
  `id` bigint(64) NOT NULL,
  `member_type` enum('node','way','relation') NOT NULL default 'node',
  `member_id` bigint(11) NOT NULL,
  `member_role` varchar(255) NOT NULL default '',
  `sequence_id` int(11) NOT NULL default '0',
  PRIMARY KEY  (`id`,`member_type`,`member_id`,`member_role`,`sequence_id`),
  KEY `current_relation_members_member_idx` (`member_type`,`member_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `current_relation_tags`
--

DROP TABLE IF EXISTS `current_relation_tags`;
CREATE TABLE IF NOT EXISTS `current_relation_tags` (
  `id` bigint(64) NOT NULL,
  `k` varchar(255) NOT NULL default '',
  `v` varchar(255) NOT NULL default '',
  PRIMARY KEY  (`id`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `current_ways`
--

DROP TABLE IF EXISTS `current_ways`;
CREATE TABLE IF NOT EXISTS `current_ways` (
  `id` bigint(64) NOT NULL auto_increment,
  `changeset_id` bigint(20) NOT NULL,
  `timestamp` datetime NOT NULL,
  `visible` tinyint(1) NOT NULL,
  `version` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `current_ways_timestamp_idx` (`timestamp`),
  KEY `changeset_id` (`changeset_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=31336923 ;

-- --------------------------------------------------------

--
-- Структура табліцы `current_way_nodes`
--

DROP TABLE IF EXISTS `current_way_nodes`;
CREATE TABLE IF NOT EXISTS `current_way_nodes` (
  `id` bigint(64) NOT NULL,
  `node_id` bigint(64) NOT NULL,
  `sequence_id` bigint(11) NOT NULL,
  PRIMARY KEY  (`id`,`sequence_id`),
  KEY `current_way_nodes_node_idx` (`node_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `current_way_tags`
--

DROP TABLE IF EXISTS `current_way_tags`;
CREATE TABLE IF NOT EXISTS `current_way_tags` (
  `id` bigint(64) NOT NULL,
  `k` varchar(255) NOT NULL default '',
  `v` varchar(255) NOT NULL default '',
  PRIMARY KEY  (`id`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `diary_comments`
--

DROP TABLE IF EXISTS `diary_comments`;
CREATE TABLE IF NOT EXISTS `diary_comments` (
  `id` bigint(20) NOT NULL auto_increment,
  `diary_entry_id` bigint(20) NOT NULL,
  `user_id` bigint(20) NOT NULL,
  `body` text NOT NULL,
  `created_at` datetime NOT NULL,
  `updated_at` datetime NOT NULL,
  PRIMARY KEY  (`id`),
  UNIQUE KEY `diary_comments_entry_id_idx` (`diary_entry_id`,`id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `diary_entries`
--

DROP TABLE IF EXISTS `diary_entries`;
CREATE TABLE IF NOT EXISTS `diary_entries` (
  `id` bigint(20) NOT NULL auto_increment,
  `user_id` bigint(20) NOT NULL,
  `title` varchar(255) NOT NULL,
  `body` text NOT NULL,
  `created_at` datetime NOT NULL,
  `updated_at` datetime NOT NULL,
  `latitude` double default NULL,
  `longitude` double default NULL,
  `language` varchar(3) default NULL,
  PRIMARY KEY  (`id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `friends`
--

DROP TABLE IF EXISTS `friends`;
CREATE TABLE IF NOT EXISTS `friends` (
  `id` bigint(20) NOT NULL auto_increment,
  `user_id` bigint(20) NOT NULL,
  `friend_user_id` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `user_id_idx` (`friend_user_id`),
  KEY `friends_user_id_idx` (`user_id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `gps_points`
--

DROP TABLE IF EXISTS `gps_points`;
CREATE TABLE IF NOT EXISTS `gps_points` (
  `altitude` float default NULL,
  `trackid` int(11) NOT NULL,
  `latitude` int(11) NOT NULL,
  `longitude` int(11) NOT NULL,
  `gpx_id` bigint(64) NOT NULL,
  `timestamp` datetime default NULL,
  `tile` int(10) unsigned NOT NULL,
  KEY `points_gpxid_idx` (`gpx_id`),
  KEY `points_tile_idx` (`tile`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `gpx_files`
--

DROP TABLE IF EXISTS `gpx_files`;
CREATE TABLE IF NOT EXISTS `gpx_files` (
  `id` bigint(64) NOT NULL auto_increment,
  `user_id` bigint(20) NOT NULL,
  `visible` tinyint(1) NOT NULL default '1',
  `name` varchar(255) NOT NULL default '',
  `size` bigint(20) default NULL,
  `latitude` double default NULL,
  `longitude` double default NULL,
  `timestamp` datetime NOT NULL,
  `public` tinyint(1) NOT NULL default '1',
  `description` varchar(255) NOT NULL default '',
  `inserted` tinyint(1) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `gpx_files_timestamp_idx` (`timestamp`),
  KEY `gpx_files_visible_public_idx` (`visible`,`public`),
  KEY `gpx_files_user_id_idx` (`user_id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `gpx_file_tags`
--

DROP TABLE IF EXISTS `gpx_file_tags`;
CREATE TABLE IF NOT EXISTS `gpx_file_tags` (
  `gpx_id` bigint(64) NOT NULL default '0',
  `tag` varchar(255) NOT NULL,
  `id` bigint(20) NOT NULL auto_increment,
  PRIMARY KEY  (`id`),
  KEY `gpx_file_tags_gpxid_idx` (`gpx_id`),
  KEY `gpx_file_tags_tag_idx` (`tag`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `messages`
--

DROP TABLE IF EXISTS `messages`;
CREATE TABLE IF NOT EXISTS `messages` (
  `id` bigint(20) NOT NULL auto_increment,
  `from_user_id` bigint(20) NOT NULL,
  `title` varchar(255) NOT NULL,
  `body` text NOT NULL,
  `sent_on` datetime NOT NULL,
  `message_read` tinyint(1) NOT NULL default '0',
  `to_user_id` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `messages_to_user_id_idx` (`to_user_id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `nodes`
--

DROP TABLE IF EXISTS `nodes`;
CREATE TABLE IF NOT EXISTS `nodes` (
  `id` bigint(64) NOT NULL,
  `latitude` int(11) NOT NULL,
  `longitude` int(11) NOT NULL,
  `changeset_id` bigint(20) NOT NULL,
  `visible` tinyint(1) NOT NULL,
  `timestamp` datetime NOT NULL,
  `tile` int(10) unsigned NOT NULL,
  `version` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`,`version`),
  KEY `nodes_timestamp_idx` (`timestamp`),
  KEY `nodes_tile_idx` (`tile`),
  KEY `changeset_id` (`changeset_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `node_tags`
--

DROP TABLE IF EXISTS `node_tags`;
CREATE TABLE IF NOT EXISTS `node_tags` (
  `id` bigint(64) NOT NULL,
  `version` bigint(20) NOT NULL,
  `k` varchar(255) NOT NULL default '',
  `v` varchar(255) NOT NULL default '',
  PRIMARY KEY  (`id`,`version`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `relations`
--

DROP TABLE IF EXISTS `relations`;
CREATE TABLE IF NOT EXISTS `relations` (
  `id` bigint(64) NOT NULL default '0',
  `changeset_id` bigint(20) NOT NULL,
  `timestamp` datetime NOT NULL,
  `version` bigint(20) NOT NULL,
  `visible` tinyint(1) NOT NULL default '1',
  PRIMARY KEY  (`id`,`version`),
  KEY `relations_timestamp_idx` (`timestamp`),
  KEY `changeset_id` (`changeset_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `relation_members`
--

DROP TABLE IF EXISTS `relation_members`;
CREATE TABLE IF NOT EXISTS `relation_members` (
  `id` bigint(64) NOT NULL default '0',
  `member_type` enum('node','way','relation') NOT NULL default 'node',
  `member_id` bigint(11) NOT NULL,
  `member_role` varchar(255) NOT NULL default '',
  `version` bigint(20) NOT NULL default '0',
  `sequence_id` int(11) NOT NULL default '0',
  PRIMARY KEY  (`id`,`version`,`member_type`,`member_id`,`member_role`,`sequence_id`),
  KEY `relation_members_member_idx` (`member_type`,`member_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `relation_tags`
--

DROP TABLE IF EXISTS `relation_tags`;
CREATE TABLE IF NOT EXISTS `relation_tags` (
  `id` bigint(64) NOT NULL default '0',
  `k` varchar(255) NOT NULL default '',
  `v` varchar(255) NOT NULL default '',
  `version` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`,`version`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `schema_migrations`
--

DROP TABLE IF EXISTS `schema_migrations`;
CREATE TABLE IF NOT EXISTS `schema_migrations` (
  `version` varchar(255) NOT NULL,
  UNIQUE KEY `unique_schema_migrations` (`version`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `sessions`
--

DROP TABLE IF EXISTS `sessions`;
CREATE TABLE IF NOT EXISTS `sessions` (
  `id` int(11) NOT NULL auto_increment,
  `session_id` varchar(255) default NULL,
  `data` text,
  `created_at` datetime default NULL,
  `updated_at` datetime default NULL,
  PRIMARY KEY  (`id`),
  UNIQUE KEY `sessions_session_id_idx` (`session_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=2 ;

-- --------------------------------------------------------

--
-- Структура табліцы `users`
--

DROP TABLE IF EXISTS `users`;
CREATE TABLE IF NOT EXISTS `users` (
  `email` varchar(255) NOT NULL,
  `id` bigint(20) NOT NULL auto_increment,
  `active` int(11) NOT NULL default '0',
  `pass_crypt` varchar(255) NOT NULL,
  `creation_time` datetime NOT NULL,
  `display_name` varchar(255) NOT NULL default '',
  `data_public` tinyint(1) NOT NULL default '0',
  `description` text NOT NULL,
  `home_lat` double default NULL,
  `home_lon` double default NULL,
  `home_zoom` smallint(6) default '3',
  `nearby` int(11) default '50',
  `pass_salt` varchar(255) default NULL,
  `image` text,
  `administrator` tinyint(1) NOT NULL default '0',
  `email_valid` tinyint(1) NOT NULL default '0',
  `new_email` varchar(255) default NULL,
  `visible` tinyint(1) NOT NULL default '1',
  `creation_ip` varchar(255) default NULL,
  PRIMARY KEY  (`id`),
  UNIQUE KEY `users_email_idx` (`email`),
  UNIQUE KEY `users_display_name_idx` (`display_name`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=101442 ;

-- --------------------------------------------------------

--
-- Структура табліцы `user_preferences`
--

DROP TABLE IF EXISTS `user_preferences`;
CREATE TABLE IF NOT EXISTS `user_preferences` (
  `user_id` bigint(20) NOT NULL,
  `k` varchar(255) NOT NULL,
  `v` varchar(255) NOT NULL,
  PRIMARY KEY  (`user_id`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `user_tokens`
--

DROP TABLE IF EXISTS `user_tokens`;
CREATE TABLE IF NOT EXISTS `user_tokens` (
  `id` bigint(20) NOT NULL auto_increment,
  `user_id` bigint(20) NOT NULL,
  `token` varchar(255) NOT NULL,
  `expiry` datetime NOT NULL,
  PRIMARY KEY  (`id`),
  UNIQUE KEY `user_tokens_token_idx` (`token`),
  KEY `user_tokens_user_id_idx` (`user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;

-- --------------------------------------------------------

--
-- Структура табліцы `ways`
--

DROP TABLE IF EXISTS `ways`;
CREATE TABLE IF NOT EXISTS `ways` (
  `id` bigint(64) NOT NULL default '0',
  `changeset_id` bigint(20) NOT NULL,
  `timestamp` datetime NOT NULL,
  `version` bigint(20) NOT NULL,
  `visible` tinyint(1) NOT NULL default '1',
  PRIMARY KEY  (`id`,`version`),
  KEY `ways_timestamp_idx` (`timestamp`),
  KEY `changeset_id` (`changeset_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `way_nodes`
--

DROP TABLE IF EXISTS `way_nodes`;
CREATE TABLE IF NOT EXISTS `way_nodes` (
  `id` bigint(64) NOT NULL,
  `node_id` bigint(64) NOT NULL,
  `version` bigint(20) NOT NULL,
  `sequence_id` bigint(11) NOT NULL,
  PRIMARY KEY  (`id`,`version`,`sequence_id`),
  KEY `way_nodes_node_idx` (`node_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- Структура табліцы `way_tags`
--

DROP TABLE IF EXISTS `way_tags`;
CREATE TABLE IF NOT EXISTS `way_tags` (
  `id` bigint(64) NOT NULL default '0',
  `k` varchar(255) NOT NULL,
  `v` varchar(255) NOT NULL,
  `version` bigint(20) NOT NULL,
  PRIMARY KEY  (`id`,`version`,`k`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Абмежаваньні для экспартаваных табліц
--

--
-- Абмежаваньні для табліцы `current_nodes`
--
ALTER TABLE `current_nodes`
  ADD CONSTRAINT `current_nodes_ibfk_1` FOREIGN KEY (`changeset_id`) REFERENCES `changesets` (`id`);

--
-- Абмежаваньні для табліцы `current_node_tags`
--
ALTER TABLE `current_node_tags`
  ADD CONSTRAINT `current_node_tags_ibfk_1` FOREIGN KEY (`id`) REFERENCES `current_nodes` (`id`);

--
-- Абмежаваньні для табліцы `current_relations`
--
ALTER TABLE `current_relations`
  ADD CONSTRAINT `current_relations_ibfk_1` FOREIGN KEY (`changeset_id`) REFERENCES `changesets` (`id`);

--
-- Абмежаваньні для табліцы `current_relation_members`
--
ALTER TABLE `current_relation_members`
  ADD CONSTRAINT `current_relation_members_ibfk_1` FOREIGN KEY (`id`) REFERENCES `current_relations` (`id`);

--
-- Абмежаваньні для табліцы `current_relation_tags`
--
ALTER TABLE `current_relation_tags`
  ADD CONSTRAINT `current_relation_tags_ibfk_1` FOREIGN KEY (`id`) REFERENCES `current_relations` (`id`);

--
-- Абмежаваньні для табліцы `current_ways`
--
ALTER TABLE `current_ways`
  ADD CONSTRAINT `current_ways_ibfk_1` FOREIGN KEY (`changeset_id`) REFERENCES `changesets` (`id`);

--
-- Абмежаваньні для табліцы `current_way_nodes`
--
ALTER TABLE `current_way_nodes`
  ADD CONSTRAINT `current_way_nodes_ibfk_2` FOREIGN KEY (`node_id`) REFERENCES `current_nodes` (`id`),
  ADD CONSTRAINT `current_way_nodes_ibfk_1` FOREIGN KEY (`id`) REFERENCES `current_ways` (`id`);

--
-- Абмежаваньні для табліцы `current_way_tags`
--
ALTER TABLE `current_way_tags`
  ADD CONSTRAINT `current_way_tags_ibfk_1` FOREIGN KEY (`id`) REFERENCES `current_ways` (`id`);

--
-- Абмежаваньні для табліцы `nodes`
--
ALTER TABLE `nodes`
  ADD CONSTRAINT `nodes_ibfk_1` FOREIGN KEY (`changeset_id`) REFERENCES `changesets` (`id`);

--
-- Абмежаваньні для табліцы `node_tags`
--
ALTER TABLE `node_tags`
  ADD CONSTRAINT `node_tags_ibfk_1` FOREIGN KEY (`id`, `version`) REFERENCES `nodes` (`id`, `version`);

--
-- Абмежаваньні для табліцы `relations`
--
ALTER TABLE `relations`
  ADD CONSTRAINT `relations_ibfk_1` FOREIGN KEY (`changeset_id`) REFERENCES `changesets` (`id`);

--
-- Абмежаваньні для табліцы `relation_members`
--
ALTER TABLE `relation_members`
  ADD CONSTRAINT `relation_members_ibfk_1` FOREIGN KEY (`id`, `version`) REFERENCES `relations` (`id`, `version`);

--
-- Абмежаваньні для табліцы `relation_tags`
--
ALTER TABLE `relation_tags`
  ADD CONSTRAINT `relation_tags_ibfk_1` FOREIGN KEY (`id`, `version`) REFERENCES `relations` (`id`, `version`);

--
-- Абмежаваньні для табліцы `ways`
--
ALTER TABLE `ways`
  ADD CONSTRAINT `ways_ibfk_1` FOREIGN KEY (`changeset_id`) REFERENCES `changesets` (`id`);

--
-- Абмежаваньні для табліцы `way_nodes`
--
ALTER TABLE `way_nodes`
  ADD CONSTRAINT `way_nodes_ibfk_1` FOREIGN KEY (`id`, `version`) REFERENCES `ways` (`id`, `version`);

--
-- Абмежаваньні для табліцы `way_tags`
--
ALTER TABLE `way_tags`
  ADD CONSTRAINT `way_tags_ibfk_1` FOREIGN KEY (`id`, `version`) REFERENCES `ways` (`id`, `version`);
```


<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>


{% @marketo/form formId="4316" %}
