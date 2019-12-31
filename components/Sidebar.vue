<template>
  <div class="sidebar --row">
    <div class="--row --m3">
        <span class="t3 --m1">
        Donate
        </span>
        <p>Your donation matters. Click below for secure online giving through Virgin or for our donation form.</p>
        <a href="http://uk.virginmoneygiving.com/charities/TheLAST SurgeryTrust" target="_blank">
          <img
          height="85px"
          width="211px"
          src="@/assets/images/donate.jpg"
          alt="Donate"
          title="Make a donation through Virgin Money Giving"
        >
        </a>
    </div>
    <div class="--row --m3">
        <span class="t3 --m1">
        Direct Donations
        </span>
        <p>You can also donate directly to the LAST Surgery trust simply download and return <a href="/Ameca-donation-form.pdf" target="_blank">this PDF form.</a></p>
    </div>
  </div>
</template>

<style scoped>
.sidebar p a {
  display: inline-block;
}
.sidebar img{
    width: auto;
    height: auto;
    max-width: 100%;
}
.sidebar ul{
  color: #000;
  font-size: 15px;
  line-height: 30px;
  margin: 0 0 10px 0;
  list-style-type: disc;
}
.sidebar form input {
    display: block;
    width: 100%;
    outline: 0;
    border: 1px solid #ccc;
    padding: 5px 0;
}
.sidebar form input[type="submit"] {
    background: transparent;
    border: 1px solid #d6aa77;
    color: #d6aa77;
    padding: 10px;
    text-transform: uppercase;
    font-weight: 600;
}
</style>
