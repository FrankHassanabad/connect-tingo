# connect-tingo

  TingoDB session store for Connect.  This is a complete copy of [connect-mongo](https://github.com/kcbanner/connect-mongo),
  but using [tingo](https://github.com/sergeyksv/tingodb) instead.

## Installation

connect-tingo supports only connect `>= 1.0.3`.

via npm:

    $ npm install connect-tingo

## Example

With express:

    var express = require('express');
    var TingoStore = require('connect-tingo')(express);

    app.use(express.session({
        secret: settings.cookie_secret,
        store: new TingoStore({
          db: settings.folderLocation
        })
      }));

With connect:

    var connect = require('connect');
    var TingoStore = require('connect-tingo')(connect);

## Removing expired sessions

  connect-tingo uses TingoDB's TTL collection feature (2.2+) to
  have tingodb automatically remove expired sessions. (tingodb runs this
  check every minute.)

  **Note:** By connect/express's default, session cookies are set to 
  expire when the user closes their browser (maxAge: null). In accordance
  with standard industry practices, connect-tingo will set these sessions
  to expire two weeks from their last 'set'. You can override this 
  behavior by manually setting the maxAge for your cookies -- just keep in
  mind that any value less than 60 seconds is pointless, as tingodb will
  only delete expired documents in a TTL collection every minute.

  For more information, consult connect's [session documentation](http://www.senchalabs.org/connect/session.html)
