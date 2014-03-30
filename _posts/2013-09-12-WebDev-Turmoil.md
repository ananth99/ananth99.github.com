---
layout: post
title: "WebDev Turmoil"
description: "Path of the Web Developer Episode I"
category:
tags: [Databases, Startups,Yii]
---

Repeat after me...

####"DATABASE MIGRATION IS AS IMPORTANT AS HAVING A VCS."
If you're a newbie who's into WebDev like me, the above mantra should be the 1st one of your 108 mantras. 

I'm currently working as a developer in a small startup. We're a team of four and we are working with the LAMP technology stack. Let me tell you why I'm writing this post..

I did a feature implementation few days back and had created a couple of models and did a whole lot of tweaking in that process to the Database. Had this been just a code change which had to do with the Controllers or Views, we could've easily version-ed the code using *[git](http://git-scm.com/)* or any other *[vcs](http://en.wikipedia.org/wiki/Revision_control)*. But this Database tweak needed a Migration to be done and we didn't have that in our code. Result? I pushed my code yesterday and my boss is still finding out the differences in the Database. We are due to do a Beta Release by EOD today and at this rate I think it's highly unlikely that it'll happen. So here I am, sitting at my desk just blinking at the monitor for the last four hours, ranting why it's a thumb rule or a best practice to create a Migration immediately after you come up with your schema.

#### Update

I've tried to explain on how to create a Migration for your App that is developed using the *[Yii Framework](www.yiiframework.com)*.

To start off with, let's define the Thumb Rule in Database Migration. Any change(creating a table, removing a column, adding column constraints etc etc), that needs to be done to the existing structure of the Database, needs to be versioned. That said, let's look into some code snippets to understand this better. Let's assume that we have 2 developers A and B who are working on an exciting product. 

##### Scenario

A wants to create a new table. So, he opens his terminal and keys in the following code.
{% highlight vim%}
$php yiic migrate create add_demo_table
{% endhighlight %}

The code creates a skeleton of the Migration he wishes to create.

###### m131122_184424_add_demo_table.php

{%highlight vim%}
<?php
class m131122_184424_add_demo_table extends CDbMigration
{
	public function up()
	{
	}

	public function down()
	{
		echo "m131122_184424_add_demo_table does not support migration down.\n";
		return false;
	}

	/*
	// Use safeUp/safeDown to do migration with transaction
	public function safeUp()
	{
	}

	public function safeDown()
	{
	}
	*/
}
?>
{% endhighlight %}

The naming is the essential part since the Database is versioned according to the time the migration is created. Now A can write his create table statements inside the up() function or the safeUp() function like this:

{%highlight vim%}
$this->createTable("demo_table",array(
	'id'=>'integer not null',
	'name'=>'varchar(255) not null',
	'primary key(id)',
	)
);
{% endhighlight %}

So, now, if B wants to add a column to this table the next day, he simply creates another migration like this:
{% highlight vim%}
$php yiic migrate create add_column_to_demo_table
{% endhighlight %}

Thus all your Database tweaking is essentially version controlled! Now, if C joins the team, all he has to do is to copy all the migration files
and fire this command in the terminal:

{% highlight vim%}
$php yiic migrate up
{% endhighlight %}

Voila! He now has the most recent version of the Database. It's that simple. :-)

To undo the last migrate operation:

{% highlight vim%}
$php yiic migrate down
{% endhighlight %}

The above command just invokes the down() or the safeDown() method which generally contains drop table commands.

Note that when you're firing the terminal commands, make sure you're inside the protected folder. Otherwise, the yiic migrate tool won't work.

Almost every framework today, supports Migration. So, whichever framework you're working on, make sure you create and update your Migration whenever you play around with your Database. Happy developing!  

May the Force be with You!