# Uppgift 5 - Networking

Under denna vecka ska ni implementera nätverksprotokollet som ni utvecklade
under övningen för att kunna spela mot varandra över ett nätverk med era
schackspel. Ert program ska *både* kunna ansluta till en motståndare och ta emot
anslutningar. Specifikationen för protokollet finns [här](https://github.com/INDA25PlusPlus/chesstp-spec).
Det går bra att välja server-/klientroll med en flagga på kommandoraden (ni behöver
alltså inte lägga till nån slags grafisk meny eller dylikt).


För att använda TCP i Rust behöver ni ha koll på dessa structs:
* [`std::net::TcpListener`](https://doc.rust-lang.org/std/net/struct.TcpListener.html):
  Används för att ta emot anslutningar på serversidan.
* [`std::net::TcpStream`](https://doc.rust-lang.org/std/net/struct.TcpStream.html):
  Används på båda sidor för att läsa och skriva data.


Eftersom ni både ska köra era vanliga spelslinga och
vänta på meddelanden samtidigt, kan det vara bra att
sätta "non-blocking" mode på TCP-streamen. Dokumentation
för detta finns [här](https://doc.rust-lang.org/std/net/struct.TcpStream.html#method.set_nonblocking)
(observera hanteringen av felkoden `WouldBlock`).


Ni fortsätter arbeta med de repon ni skapade i förra uppgiften (`kth_id-gui`).


Lycka till!
