<script>
    import "../global.css";
    import logo from '$lib/images/logo.png';
    import telegram from "$lib/images/telegram.png";
</script>

<header class="header">
    <base href="/BookClub-app/">
    <img src={logo} class="logo" alt="The logo">
    <nav class="nav-links">
        <ul>
            <li><a href="/">Main page</li>
            <li><a href="/BookCrossingPage">Book crossing</a></li>
            <li><a href="/BlogPagePublic">Blog</a></li>
            <li><a href="/EventsPage">Events</a></li>
            <li><a href="/LoginPage">Log in</a></li>
            <li><a href="https://t.me/innobooklovers"><img class="telegram" src={telegram} alt="The telegram channel link"></a></li>
        </ul>
    </nav>
</header>

<slot/>

<style>
    .nav-links {
        
    }
</style>