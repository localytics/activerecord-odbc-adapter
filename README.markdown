# OpenLink ODBC Data Adapter for Ruby on Rails

(C) 2008 OpenLink Software


# Status

**23-Nov-2015**
  * Update fetch query results

**19-Nov-2015**

Update to preserve limits on queries
Update to add query comments

**26-Jun-2015**

Added support for Rails 4.2

**12-Sep-2012**

Added support for Rails / ActiveRecord 3.1.x and 3.2

**22-Nov-2008**

Added new install information

**23-Apr-2008**

The adapter has been updated to support Rails 2.0.2 / ActiveRecord 2.0.2
The new adapter (v2.0) is not recommended for use with earlier releases of
Rails or ActiveRecord.

* For Rails 2.0.2 / ActiveRecord 2.0.2 or later, use odbc-rails v2.0
* For Rails 1.2.x / ActiveRecord 1.15.x, use odbc-rails v1.5
* For Rails 1.1.x / ActiveRecord 1.14.x, use odbc-rails v1.3

The configuration instructions for v1.4 or earlier differ slightly from those
included here for v2.0. Please refer to the documentation packaged with the
respective adapter when using the previous releases.

Added support for DSN-less connections (thanks to Ralf Vitasek).
Added support for SQLAnywhere (thanks to Bryan Lahartinger).

**23-Feb-2007**

The adapter has been updated to support Rails 1.2.x / ActiveRecord 1.15.x.
The new adapter (v1.4) is not recommended for use with Rails 1.1 / ActiveRecord
1.14.x. Please use v1.3 of the adapter with Rails 1.1.

The driver now supports the new ActiveRecord :decimal type and an
:emulate_booleans connection option. See http://odbc-rails.rubyforge.org for
more information about this option.

**09-Jan-2007**

The adapter accompanying this note is a Generic ODBC Adapter for Ruby on Rails
being developed by **OpenLink&nbsp;Software**[http://www.openlinksw.com].

The aim of this development is to provide a single ODBC-based adapter
capable of supporting the most popular DBMSes, in contrast to the
current approach in the Rails community of each database requiring
its own adapter.

It currently supports Ingres r3, Informix 9.3 or later, Oracle 10g,
MySQL 5 and OpenLink's Virtuoso
(Open&nbsp;Source&nbsp;Edition[http://virtuoso.openlinksw.com]),
SQL Server 2000/2005, Sybase ASE 15, DB2 v9, Progress v8/9/10 and PostgreSQL 8.2.

Testing to date has been limited to the ROR 'Expenses' sample
application described at http://developer.apple.com/tools/rubyonrails.html
and the ActiveRecord test modules base_test.rb and migration_test.rb.

Testing has been performed on Linux, Windows and Mac OS X using
OpenLink's own ODBC drivers and the native Virtuoso ODBC client.


# Pre-Requisites

The OpenLink ODBC Adapter for Ruby on Rails needs the
ActiveRecord[http://wiki.rubyonrails.com/rails/pages/ActiveRecord]
package installed.

The Adapter also requires Christian Werner's
Ruby&nbsp;ODBC&nbsp;Bridge[http://www.ch-werner.de/rubyodbc]
(release 0.9991 or later), to bridge to an underlying ODBC driver.


# Contents

In the accompanying sources, the lib directory structure is equivalent
to the lib directory located under ACTIVE_RECORD_ROOT in your main
Ruby tree.

On Windows ACTIVE_RECORD_ROOT will be something like:

    c:\ruby\lib\ruby\gems\1.8\gems\activerecord-x.y.z

On Unix and Mac OS X ACTIVE_RECORD_ROOT will be something like:

    /usr/lib/ruby/gems/1.8/gems/activerecord-x.y.z
or
    /usr/local/lib/ruby/gems/1.8/gems/activerecord-x.y.z

On Mac OS X using Locomotive ACTIVE_RECORD_ROOT will be
something like:

    /Applications/Locomotive2/bundles/rails112.locobundle/i386/lib/ruby/gems/1.8/gems/activerecord-x.y.z

lib/ contains the files which constitute the new ODBC adapter.

test/ contains the fixture definitions for testing the adapter.

support/odbc_rails.diff contains some patches to ActiveRecord tests.

The patches to base_test.rb and migration_test.rb are not essential.
However, they modify or bypass certain tests to cope with limitations
of particular databases. Other developers have previously modified
the tests similarly to cope with limitations of other Rails-supported
databases. The patched versions of files touched by odbc_rails.diff can
be found in support/test.

# Installation

There are 3 ways to install the ODBC Adapter package: either as a gem
(recommended), a plugin, or by running the custom installation script. Pick
one of the following, depending on whether you want the adapter to be
available system-wide or just within a particular Rails project.

# Installation as a Gem (recommended)

* If you haven't done so already first add github to rubygems with:

  gem sources -a http://gems.github.com

* Install the odbc-rails gem by running:

  gem install -r dosire-activerecord-odbc-adapter --include-dependencies

# Installation as a Plugin

Installing the OpenLink ODBC Data Adapter as a plugin makes it available to
a particular Rails application only.

# Automatic Plugin installation

The adapter can be automatically installed as a plugin by navigating to the
root of your Rails application and typing either:

    script/plugin install odbc-rails
or
    script/plugin install http://odbc-rails.rubyforge.org/plugins/odbc-rails

On Windows, replace <tt>script/plugin</tt> by <tt>ruby script/plugin</tt>.
e.g. <tt>ruby script/plugin install odbc-rails</tt>


# Manual Plugin Installation

You can also install the plugin manually by unpacking the sources into the
vendor/plugins directory of your Rails application.

# Custom installation script

When using <tt>rake install</tt> or running the install_odbc.rb script by
hand, the script tries to determine the location of the activerecord
package within your Ruby installation and allows you to overrule the
directory it has found with a directory of your choice. If more than one
version of activerecord is found, the default will be the latest version.

On Mac OS X the installation script is also capable of locating Locomotive,
if installed, and will ask to install in there.

The install_odbc.rb script also verifies that the pre-requisites are
installed.

If all else fails this document also describes the steps to install the
ODBC adapter into activerecord manually.


# Using rake

The simplest way to install the adapter is by using the following
command as root:

    # rake install

or if your system supports sudo:

    $ sudo rake install


The Rakefile also defines some targets specifically for developers:

    $ rake rdoc         # Generate rdoc documentation in ~/doc

    $ rake package	# Create distribution package in ~/distrib

    $ rake clean	# Remove generated files and directories


# Running installation script

The second way of installing the adapter is running the
<tt>install_odbc.rb</tt> script as root.

    # ruby install_odbc.rb

or if your system supports sudo:

    $ sudo ruby install_odbc.rb


# Installing files manually

The third way of installing the adapter is by performing the installation
steps yourself.

* Copy odbc_adapter.rb to the ACTIVE_RECORD_ROOT/lib/active_record/connection_adapters/ directory

* Copy the odbcext_*.rb files to the ACTIVE_RECORD_ROOT/lib/active_record/vendor/ directory

# Configuring the Adapter

Examples of the required connection parameters can be found in

   test/connections/native_odbc/connection.rb

If you enable call-tracing by setting :trace #> true,  specify the
logger output file as illustrated in connection.rb, e.g.

    ActiveRecord::Base.logger # Logger.new("debug_odbc.log")

# License

The OpenLink ODBC Adapter for Ruby on Rails is released under the
MIT license as detailed in the file COPYING.


# Submitting fixes and enhancements

Patches and new contributions can be submitted as diffs from the
current CVS archive by:

    $ cvs add newfiles

    $ cvs -z3 diff -uN > diffs

Patches and  contributions can be send to the OpenLink iODBC source
archive mainainter at mailto:iodbc@openlinksw.com to be included
in the next distribution. Please provide accompanying documentation
on which bugs are fixed or new features are introduced.
