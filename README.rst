manage.py
=========

Human friendly CLI builder.

Installation
------------

``pip install manage.py``


Quickstart
----------

``cat manage.py``::

    from manage import Manager

    manager = Manager()

    @manager.command
    def echo(text, capitalyze=False):
        """print the given <name>"""
        if capitalyze:
            text = text.upper()
        return text


``manage --help``::

    usage: manage [<namespace>.]<command> [<args>]

    positional arguments:
      command     the command to run

    optional arguments:
      -h, --help  show this help message and exit

    available commands:
      echo        print the given <name>


``manage echo --help``::

    $ manage echo --help

    usage: manage [-h] [--capitalyze] text

    print the given <name>

    positional arguments:
      text          no description

    optional arguments:
      -h, --help    show this help message and exit
      --capitalyze  no description


Managers
--------

Managers can be used together by merging them::

    from third_party import manager

    my_app_manager.merge(manager)

    # Merge within a new namespace:
    my_app_manager.merge(manager, namespace='third_party')


Commands
--------

Commands can be organized within namespaces::

    @manager.command(namespace='config')
    def set(key, value):
        # ...


Arguments
---------

Argument definition can be overridden::

    @manager.arg('first_arg', help='this is help for first arg')
    @manager.command
    def my_command(first_arg):
        # ...
