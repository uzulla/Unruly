# NAME

Unruly - It's new $module

# SYNOPSIS

    use Unruly;
    use AnyEvent;
    use utf8;
    

    my $cv = AnyEvent->condvar;
    

    my $c = Unruly->new(url => 'http://yancha.hachiojipm.org', tags => {PUBLIC => 1});
    $c->login('waiwai');
    

    $c->run(sub {
        my ($client, $socket) = @_;
        $socket->on('user message' => sub {
            my $message = $_[1];
            unless($message->{nickname} eq 'waiwai') {
                my @tags = @{$message->{tags}};
                if ($message->{text} =~ /ワイワイ/) {
                    $c->post('ワイワイ', @tags);
                }
            }
        });
    });
    

    $cv->wait;



# DESCRIPTION

Unruly is ...

# LICENSE

Copyright (C) ytnobody.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# AUTHOR

ytnobody <ytnobody@gmail.com>
