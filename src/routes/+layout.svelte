<script>
    import "../global.css";
</script>

<header class="header">
    <base href="/BookClub-app/">
    <!-- <img src="$lib/images/logo.png" class="logo" alt="Our logo"> -->

    <nav class="nav-links">
        <ul>
            <li>
                <div class="current"><a href="/">Main page</a></div>
            </li>
            <li><a href="/BookCrossingPage">Book crossing</a></li>
            <li><a href="/BlogPagePublic">Blog</a></li>
            <li><a href="/EventsPage">Events</a></li>
            <li><a href="/LoginPage">Log in</a></li>
            <!-- <li><a href="https://t.me/innobooklovers"><img class="telegram" src="images/telegram.png" alt="Our telegram channel link"></a></li> -->
        </ul>
    </nav>
    
</header>

<slot />
