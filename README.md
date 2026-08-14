<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>DA7</title>

<style>

:root{
    --bg:#05040a;
    --panel:rgba(12,10,23,.94);
    --card:rgba(24,20,42,.72);

    --purple:#8b5cf6;
    --purple2:#a855f7;

    --blue:#38bdf8;
    --green:#22c55e;
    --red:#ef4444;

    --text:#ffffff;
    --muted:#9692aa;

    --border:rgba(139,92,246,.28);
}

*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Inter,Arial,Helvetica,sans-serif;
}

html,body{
    width:100%;
    min-height:100%;
}

body{
    min-height:100vh;

    background:
        radial-gradient(
            circle at 20% 10%,
            rgba(139,92,246,.30),
            transparent 30%
        ),
        radial-gradient(
            circle at 90% 80%,
            rgba(56,189,248,.18),
            transparent 30%
        ),
        linear-gradient(
            135deg,
            #05040a,
            #090615,
            #05040a
        );

    color:var(--text);

    display:flex;
    justify-content:center;
    align-items:center;

    padding:15px;
    overflow-x:hidden;
}

/* =====================================================
   ABERTURA
===================================================== */

#intro{
    position:fixed;
    inset:0;
    z-index:99999;

    display:flex;
    justify-content:center;
    align-items:center;

    background:
        radial-gradient(
            circle,
            rgba(139,92,246,.18),
            transparent 45%
        ),
        #05040a;

    transition:opacity .8s ease;
}

.intro-box{
    width:90%;
    max-width:430px;
    text-align:center;
}

.intro-logo{
    font-size:70px;
    font-weight:900;
    letter-spacing:10px;

    background:
        linear-gradient(
            90deg,
            #fff,
            #c084fc,
            #38bdf8,
            #fff
        );

    background-size:300%;

    -webkit-background-clip:text;
    background-clip:text;

    color:transparent;

    animation:
        introLogo 2.5s
        infinite;
}

.intro-sub{
    margin-top:5px;

    color:#777186;

    font-size:9px;

    letter-spacing:4px;
}

.loading{
    margin-top:40px;
}

.loading-bar{
    width:100%;
    height:4px;

    border-radius:10px;

    background:#211d2d;

    overflow:hidden;
}

.loading-fill{
    width:0%;
    height:100%;

    background:
        linear-gradient(
            90deg,
            var(--purple),
            var(--blue)
        );

    box-shadow:
        0 0 15px
        rgba(139,92,246,.7);
}

.loading-text{
    margin-top:9px;

    color:#c084fc;

    font-size:10px;
    font-weight:800;
}

.social-intro{
    margin-top:30px;

    display:flex;
    flex-direction:column;

    gap:7px;
}

.social-intro span{
    color:#777186;

    font-size:8px;

    letter-spacing:2px;
}

.social-intro strong{
    font-size:13px;
}

@keyframes introLogo{

    0%,100%{
        background-position:0% 50%;
        transform:scale(1);
    }

    50%{
        background-position:100% 50%;
        transform:scale(1.04);
    }
}

/* =====================================================
   PARTICLES
===================================================== */

.particles{
    position:fixed;
    inset:0;

    pointer-events:none;

    overflow:hidden;

    z-index:-1;
}

.particle{
    position:absolute;

    width:3px;
    height:3px;

    border-radius:50%;

    background:var(--purple2);

    box-shadow:
        0 0 10px
        var(--purple2);

    opacity:.5;

    animation:
        floatParticle
        linear
        infinite;
}

@keyframes floatParticle{

    from{
        transform:
            translateY(110vh)
            translateX(0);
    }

    to{
        transform:
            translateY(-10vh)
            translateX(80px);
    }
}

/* =====================================================
   PAINEL
===================================================== */

.panel{
    width:420px;
    max-width:100%;

    max-height:94vh;

    overflow-y:auto;

    background:
        linear-gradient(
            145deg,
            rgba(16,12,30,.96),
            rgba(7,8,16,.95)
        );

    border:
        1px solid
        rgba(168,85,247,.35);

    border-radius:24px;

    box-shadow:

        0 0 35px
        rgba(139,92,246,.18),

        0 25px 100px
        rgba(0,0,0,.75);

    backdrop-filter:
        blur(22px);

    scrollbar-width:thin;

    scrollbar-color:
        var(--purple)
        transparent;
}

/* =====================================================
   HEADER
===================================================== */

.header{
    position:sticky;

    top:0;

    z-index:10;

    padding:18px;

    display:flex;

    justify-content:space-between;

    align-items:center;

    background:
        rgba(10,8,19,.88);

    backdrop-filter:
        blur(20px);

    border-bottom:
        1px solid
        rgba(139,92,246,.2);
}

.brand{
    display:flex;

    align-items:center;

    gap:11px;
}

.logo-icon{
    width:42px;
    height:42px;

    display:flex;

    align-items:center;
    justify-content:center;

    border-radius:13px;

    background:
        linear-gradient(
            135deg,
            var(--purple),
            var(--blue)
        );

    box-shadow:
        0 0 25px
        rgba(139,92,246,.45);

    font-size:21px;
}

.logo{
    font-size:23px;

    font-weight:900;

    letter-spacing:2px;

    background:
        linear-gradient(
            90deg,
            #fff,
            #c084fc,
            #38bdf8
        );

    -webkit-background-clip:text;
    background-clip:text;

    color:transparent;
}

.subtitle{
    margin-top:3px;

    color:var(--muted);

    font-size:9px;

    letter-spacing:1px;

    text-transform:uppercase;
}

.header-buttons{
    display:flex;

    gap:7px;
}

.icon{
    width:35px;
    height:35px;

    border:
        1px solid
        rgba(139,92,246,.25);

    border-radius:10px;

    background:
        rgba(255,255,255,.05);

    color:white;

    cursor:pointer;

    transition:.2s;
}

.icon:hover{
    background:
        rgba(139,92,246,.2);

    transform:
        translateY(-2px);
}

/* =====================================================
   CONTENT
===================================================== */

.content{
    padding:15px;
}

.section{
    margin-bottom:20px;
}

.section-title{
    display:flex;

    align-items:center;

    gap:7px;

    color:#bbb4d2;

    font-size:10px;

    font-weight:800;

    letter-spacing:1.5px;

    text-transform:uppercase;

    margin-bottom:9px;
}

/* =====================================================
   SEARCH
===================================================== */

.search{
    width:100%;

    padding:13px 14px;

    border-radius:12px;

    border:
        1px solid
        rgba(139,92,246,.25);

    background:
        rgba(255,255,255,.035);

    color:white;

    outline:none;

    transition:.2s;

    margin-bottom:9px;
}

.search::placeholder{
    color:#686379;
}

.search:focus{
    border-color:
        var(--purple);

    box-shadow:
        0 0 15px
        rgba(139,92,246,.15);
}

/* =====================================================
   PLAYERS
===================================================== */

.players{
    max-height:175px;

    overflow-y:auto;
}

.player{
    padding:11px;

    border-radius:13px;

    background:
        linear-gradient(
            135deg,
            rgba(255,255,255,.045),
            rgba(255,255,255,.015)
        );

    border:
        1px solid
        rgba(255,255,255,.06);

    margin-bottom:7px;

    display:flex;

    align-items:center;

    justify-content:space-between;

    cursor:pointer;

    transition:.2s;
}

.player:hover{
    transform:
        translateX(3px);

    border-color:
        rgba(168,85,247,.5);

    background:
        rgba(139,92,246,.08);
}

.player.selected{
    border-color:
        var(--purple);

    background:
        linear-gradient(
            90deg,
            rgba(139,92,246,.17),
            rgba(56,189,248,.06)
        );

    box-shadow:
        inset 3px 0 0
        var(--purple);
}

.player-left{
    display:flex;

    align-items:center;

    gap:10px;
}

.avatar{
    width:34px;
    height:34px;

    border-radius:10px;

    display:flex;

    align-items:center;
    justify-content:center;

    background:
        linear-gradient(
            135deg,
            var(--purple),
            var(--blue)
        );

    font-size:14px;

    font-weight:bold;
}

.player-name{
    font-size:12px;

    font-weight:700;
}

.player-id{
    margin-top:3px;

    color:var(--muted);

    font-size:9px;
}

.online{
    color:#4ade80;

    font-size:8px;

    font-weight:bold;
}

.target{
    margin-top:9px;

    padding:13px;

    border-radius:13px;

    background:
        linear-gradient(
            135deg,
            rgba(139,92,246,.11),
            rgba(56,189,248,.05)
        );

    border:
        1px solid
        rgba(139,92,246,.25);

    font-size:11px;
}

.target strong{
    color:#c084fc;

    margin-left:4px;
}

/* =====================================================
   CARDS
===================================================== */

.row{
    padding:12px;

    margin-bottom:7px;

    border-radius:13px;

    background:
        rgba(255,255,255,.035);

    border:
        1px solid
        rgba(255,255,255,.055);

    transition:.2s;
}

.row:hover{
    border-color:
        rgba(139,92,246,.25);
}

.row-flex{
    display:flex;

    align-items:center;

    justify-content:space-between;

    gap:10px;
}

.label{
    font-size:12px;

    font-weight:700;
}

.desc{
    margin-top:3px;

    color:var(--muted);

    font-size:9px;
}

/* =====================================================
   TOGGLE
===================================================== */

.toggle{
    min-width:55px;

    height:29px;

    border:none;

    border-radius:30px;

    background:#282633;

    color:#777486;

    font-size:10px;

    font-weight:900;

    cursor:pointer;

    transition:.25s;
}

.toggle.active{
    background:
        linear-gradient(
            90deg,
            var(--purple),
            var(--blue)
        );

    color:white;

    box-shadow:
        0 0 15px
        rgba(139,92,246,.35);
}

/* =====================================================
   SLIDERS
===================================================== */

.slider-head{
    display:flex;

    justify-content:space-between;

    margin-bottom:9px;

    font-size:11px;
}

.value{
    color:#c084fc;

    font-weight:900;
}

input[type="range"]{
    width:100%;

    height:4px;

    appearance:none;

    background:#292634;

    border-radius:10px;

    outline:none;
}

input[type="range"]::-webkit-slider-thumb{
    appearance:none;

    width:14px;
    height:14px;

    border-radius:50%;

    background:var(--purple2);

    box-shadow:
        0 0 12px
        rgba(168,85,247,.65);

    cursor:pointer;
}

/* =====================================================
   SELECT
===================================================== */

select{
    padding:8px 10px;

    border-radius:9px;

    border:
        1px solid
        rgba(139,92,246,.25);

    background:#191624;

    color:white;

    outline:none;
}

/* =====================================================
   BUTTONS
===================================================== */

.button{
    width:100%;

    padding:12px;

    margin-bottom:7px;

    border:
        1px solid
        rgba(139,92,246,.2);

    border-radius:12px;

    background:
        linear-gradient(
            135deg,
            rgba(139,92,246,.12),
            rgba(56,189,248,.05)
        );

    color:white;

    font-weight:800;

    font-size:11px;

    cursor:pointer;

    transition:.2s;
}

.button:hover{
    transform:
        translateY(-1px);

    border-color:
        rgba(168,85,247,.55);

    box-shadow:
        0 0 18px
        rgba(139,92,246,.15);
}

/* =====================================================
   STATUS
===================================================== */

.status{
    margin-top:4px;

    text-align:center;

    padding:10px;

    color:#6ee7a0;

    font-size:9px;

    letter-spacing:.5px;
}

/* =====================================================
   SETTINGS
===================================================== */

.settings{
    display:none;
}

.settings.open{
    display:block;
}

.setting-item{
    padding:10px;

    border-radius:11px;

    background:
        rgba(255,255,255,.03);

    margin-bottom:7px;
}

.setting-item label{
    display:block;

    color:#bbb4d2;

    font-size:10px;

    margin-bottom:6px;
}

/* =====================================================
   CODE
===================================================== */

.code-box{
    width:100%;

    min-height:180px;

    padding:12px;

    border-radius:12px;

    border:
        1px solid
        rgba(139,92,246,.25);

    background:#08070d;

    color:#a7f3d0;

    font-family:monospace;

    font-size:10px;

    resize:vertical;

    outline:none;
}

.hidden{
    display:none!important;
}

/* =====================================================
   FOOTER
===================================================== */

.footer{
    padding:12px;

    text-align:center;

    border-top:
        1px solid
        rgba(139,92,246,.15);

    color:#5f5a70;

    font-size:8px;

    letter-spacing:1px;
}

</style>
</head>

<body>

<!-- =====================================================
     MÚSICA
===================================================== -->

<audio id="introMusic" preload="auto">
    <source src="musica.mp3" type="audio/mpeg">
</audio>


<!-- =====================================================
     ABERTURA
===================================================== -->

<div id="intro">

    <div class="intro-box">

        <div class="intro-logo">
            DA7
        </div>

        <div class="intro-sub">
            PLAYER CONTROL SYSTEM
        </div>

        <div class="loading">

            <div class="loading-bar">

                <div
                    id="loadingFill"
                    class="loading-fill">
                </div>

            </div>

            <div
                id="loadingText"
                class="loading-text">
                0%
            </div>

        </div>

        <div class="social-intro">

            <span>
                SIGA NAS REDES SOCIAIS
            </span>

            <strong>
                TikTok: @otremda7
            </strong>

        </div>

    </div>

</div>


<!-- =====================================================
     PARTICLES
===================================================== -->

<div
    class="particles"
    id="particles">
</div>


<!-- =====================================================
     PAINEL
===================================================== -->

<div class="panel">

    <!-- HEADER -->

    <div class="header">

        <div class="brand">

            <div class="logo-icon">
                ⚡
            </div>

            <div>

                <div class="logo">
                    DA7
                </div>

                <div class="subtitle">
                    Player Control System
                </div>

            </div>

        </div>

        <div class="header-buttons">

            <button
                class="icon"
                onclick="minimize()">
                −
            </button>

            <button
                class="icon"
                onclick="resetSettings()">
                ↻
            </button>

        </div>

    </div>


    <div
        class="content"
        id="content">


        <!-- =================================================
             PLAYERS
        ================================================== -->

        <div class="section">

            <div class="section-title">
                👤 Players
            </div>

            <input
                id="search"
                class="search"
                placeholder="Pesquisar jogador..."
                oninput="searchPlayers()"
            >

            <div
                id="players"
                class="players">
            </div>

            <div class="target">

                🎯 Alvo selecionado:

                <strong id="target">
                    Nenhum
                </strong>

            </div>

        </div>


        <!-- =================================================
             AIM
        ================================================== -->

        <div class="section">

            <div class="section-title">
                🎯 AIM
            </div>

            <div class="row row-flex">

                <div>

                    <div class="label">
                        Lock Aim
                    </div>

                    <div class="desc">
                        Utiliza o jogador selecionado
                    </div>

                </div>

                <button
                    id="lockAim"
                    class="toggle"
                    onclick="toggle('lockAim')">

                    OFF

                </button>

            </div>


            <div class="row">

                <div class="slider-head">

                    <span>
                        FOV
                    </span>

                    <span
                        class="value"
                        id="fovText">
                        90°
                    </span>

                </div>

                <input
                    id="fov"
                    type="range"
                    min="10"
                    max="180"
                    value="90"
                    oninput="setNumber('fov',this.value)"
                >

            </div>


            <div class="row">

                <div class="slider-head">

                    <span>
                        Smooth
                    </span>

                    <span
                        class="value"
                        id="smoothText">
                        50%
                    </span>

                </div>

                <input
                    id="smooth"
                    type="range"
                    min="0"
                    max="100"
                    value="50"
                    oninput="setNumber('smooth',this.value)"
                >

            </div>

        </div>


        <!-- =================================================
             VISUAL
        ================================================== -->

        <div class="section">

            <div class="section-title">
                👁️ Visual
            </div>

            <div class="row row-flex">

                <div>

                    <div class="label">
                        ESP
                    </div>

                    <div class="desc">
                        Destaca o alvo selecionado
                    </div>

                </div>

                <button
                    id="esp"
                    class="toggle"
                    onclick="toggle('esp')">

                    OFF

                </button>

            </div>


            <div class="row row-flex">

                <div>

                    <div class="label">
                        Hitbox
                    </div>

                    <div class="desc">
                        Controle do sistema de colisão
                    </div>

                </div>

                <button
                    id="hitbox"
                    class="toggle"
                    onclick="toggle('hitbox')">

                    OFF

                </button>

            </div>


            <div class="row">

                <div class="slider-head">

                    <span>
                        Hitbox Size
                    </span>

                    <span
                        id="hitboxText"
                        class="value">
                        10
                    </span>

                </div>

                <input
                    id="hitboxSize"
                    type="range"
                    min="1"
                    max="30"
                    value="10"
                    oninput="setNumber('hitboxSize',this.value)"
                >

            </div>

        </div>


        <!-- =================================================
             MOVEMENT
        ================================================== -->

        <div class="section">

            <div class="section-title">
                ⚡ Movement
            </div>

            <div class="row row-flex">

                <div>

                    <div class="label">
                        Fly
                    </div>

                    <div class="desc">
                        Sistema de voo
                    </div>

                </div>

                <button
                    id="fly"
                    class="toggle"
                    onclick="toggle('fly')">

                    OFF

                </button>

            </div>


            <div class="row row-flex">

                <div>

                    <div class="label">
                        Speed
                    </div>

                    <div class="desc">
                        Velocidade personalizada
                    </div>

                </div>

                <button
                    id="speed"
                    class="toggle"
                    onclick="toggle('speed')">

                    OFF

                </button>

            </div>


            <div class="row">

                <div class="slider-head">

                    <span>
                        Speed
                    </span>

                    <span
                        id="speedText"
                        class="value">
                        16
                    </span>

                </div>

                <input
                    id="speedValue"
                    type="range"
                    min="1"
                    max="100"
                    value="16"
                    oninput="setNumber('speedValue',this.value)"
                >

            </div>


            <div class="row row-flex">

                <div>

                    <div class="label">
                        Sprint
                    </div>

                </div>

                <button
                    id="sprint"
                    class="toggle"
                    onclick="toggle('sprint')">

                    OFF

                </button>

            </div>

        </div>


        <!-- =================================================
             SETTINGS
        ================================================== -->

        <div class="section">

            <div class="section-title">
                ⚙️ Settings
            </div>

            <div class="row">

                <button
                    class="button"
                    onclick="toggleSettings()">

                    ⚙️ ABRIR SETTINGS

                </button>

                <div
                    id="settings"
                    class="settings">

                    <div class="setting-item">

                        <label>
                            Tema
                        </label>

                        <select
                            id="theme"
                            onchange="changeTheme(this.value)">

                            <option value="purple">
                                Purple
                            </option>

                            <option value="blue">
                                Blue
                            </option>

                            <option value="red">
                                Red
                            </option>

                            <option value="green">
                                Green
                            </option>

                        </select>

                    </div>


                    <button
                        class="button"
                        onclick="saveSettings()">

                        💾 SALVAR CONFIGURAÇÕES

                    </button>

                    <button
                        class="button"
                        onclick="resetSettings()">

                        🔄 RESETAR CONFIGURAÇÕES

                    </button>

                </div>

            </div>

        </div>


        <!-- =================================================
             LUAU
        ================================================== -->

        <div class="section">

            <div class="section-title">
                💻 Luau
            </div>

            <textarea
                id="luaCode"
                class="code-box"
                readonly>
            </textarea>

            <br><br>

            <button
                class="button"
                onclick="copyLua()">

                📋 COPIAR CONFIGURAÇÃO LUAU

            </button>

            <button
                class="button"
                onclick="downloadLua()">

                📥 BAIXAR DA7.LUA

            </button>

        </div>


        <div
            id="status"
            class="status">

            ● SISTEMA PRONTO

        </div>

    </div>


    <div class="footer">
        DA7 • TikTok @otremda7
    </div>

</div>


<script>

/* =====================================================
   ESTADO
===================================================== */

const state = {

    lockAim:false,
    esp:false,
    hitbox:false,
    fly:false,
    speed:false,
    sprint:false,

    fov:90,
    smooth:50,
    hitboxSize:10,
    speedValue:16,

    target:"Nenhum",

    theme:"purple"

};


/* =====================================================
   PARTICLES
===================================================== */

for(let i=0;i<35;i++){

    const p =
        document.createElement("div");

    p.className="particle";

    p.style.left =
        Math.random()*100+"%";

    p.style.animationDuration =
        (5+Math.random()*10)+"s";

    p.style.animationDelay =
        (-Math.random()*10)+"s";

    document
        .getElementById("particles")
        .appendChild(p);
}


/* =====================================================
   PLAYERS
===================================================== */

let players = [

    {
        name:"Player_01",
        id:"001"
    },

    {
        name:"Player_02",
        id:"002"
    },

    {
        name:"Player_03",
        id:"003"
    },

    {
        name:"Player_04",
        id:"004"
    },

    {
        name:"Player_05",
        id:"005"
    },

    {
        name:"Player_06",
        id:"006"
    }

];


function renderPlayers(list=players){

    const container =
        document.getElementById(
            "players"
        );

    container.innerHTML="";

    list.forEach(player=>{

        const div =
            document.createElement("div");

        div.className="player";

        if(
            state.target === player.name
        ){
            div.classList.add(
                "selected"
            );
        }

        div.innerHTML=`

            <div class="player-left">

                <div class="avatar">
                    ${player.name.charAt(0)}
                </div>

                <div>

                    <div class="player-name">
                        ${player.name}
                    </div>

                    <div class="player-id">
                        ID: ${player.id}
                    </div>

                </div>

            </div>

            <div class="online">
                ● ONLINE
            </div>

        `;

        div.onclick=()=>{

            state.target =
                player.name;

            document
                .getElementById(
                    "target"
                )
                .textContent =
                player.name;

            renderPlayers();

            generateLua();

            setStatus(
                "● ALVO: " +
                player.name
            );
        };

        container.appendChild(div);

    });

}


function searchPlayers(){

    const value =
        document
            .getElementById(
                "search"
            )
            .value
            .toLowerCase();

    const filtered =
        players.filter(
            p =>
                p.name
                .toLowerCase()
                .includes(value)
        );

    renderPlayers(filtered);
}


/* =====================================================
   TOGGLE
===================================================== */

function toggle(id){

    state[id]=!state[id];

    const btn =
        document.getElementById(id);

    if(state[id]){

        btn.classList.add(
            "active"
        );

        btn.textContent="ON";

    }else{

        btn.classList.remove(
            "active"
        );

        btn.textContent="OFF";

    }

    generateLua();

    setStatus(
        "● " +
        id.toUpperCase() +
        (state[id]
            ?" ATIVADO"
            :" DESATIVADO")
    );
}


/* =====================================================
   NÚMEROS
===================================================== */

function setNumber(id,value){

    state[id]=Number(value);

    if(id==="fov"){

        document
            .getElementById(
                "fovText"
            )
            .textContent =
            value+"°";
    }

    if(id==="smooth"){

        document
            .getElementById(
                "smoothText"
            )
            .textContent =
            value+"%";
    }

    if(id==="hitboxSize"){

        document
            .getElementById(
                "hitboxText"
            )
            .textContent =
            value;
    }

    if(id==="speedValue"){

        document
            .getElementById(
                "speedText"
            )
            .textContent =
            value;
    }

    generateLua();
}


/* =====================================================
   SETTINGS
===================================================== */

function toggleSettings(){

    document
        .getElementById(
            "settings"
        )
        .classList.toggle(
            "open"
        );
}


function saveSettings(){

    localStorage.setItem(
        "DA7_SETTINGS",
        JSON.stringify(state)
    );

    setStatus(
        "● CONFIGURAÇÕES SALVAS"
    );
}


function loadSettings(){

    const saved =
        localStorage.getItem(
            "DA7_SETTINGS"
        );

    if(!saved) return;

    try{

        Object.assign(
            state,
            JSON.parse(saved)
        );

    }catch(e){

        console.log(
            "Configuração inválida"
        );
    }

}


/* =====================================================
   TEMAS
===================================================== */

function changeTheme(theme){

    state.theme=theme;

    const root =
        document.documentElement;

    const themes={

        purple:{
            purple:"#8b5cf6",
            purple2:"#a855f7",
            blue:"#38bdf8"
        },

        blue:{
            purple:"#2563eb",
            purple2:"#3b82f6",
            blue:"#06b6d4"
        },

        red:{
            purple:"#dc2626",
            purple2:"#ef4444",
            blue:"#fb7185"
        },

        green:{
            purple:"#16a34a",
            purple2:"#22c55e",
            blue:"#4ade80"
        }

    };

    const t =
        themes[theme];

    root.style.setProperty(
        "--purple",
        t.purple
    );

    root.style.setProperty(
        "--purple2",
        t.purple2
    );

    root.style.setProperty(
        "--blue",
        t.blue
    );

    localStorage.setItem(
        "DA7_THEME",
        theme
    );

    generateLua();
}


/* =====================================================
   LUAU
===================================================== */

function generateLua(){

    const lua = `-- DA7
-- Configuração gerada pelo painel

local Config = {

    Target = "${state.target}",

    AIM = {

        LockAim = ${state.lockAim},
        FOV = ${state.fov},
        Smooth = ${state.smooth}

    },

    Visual = {

        ESP = ${state.esp},

        Hitbox = ${state.hitbox},

        HitboxSize = ${state.hitboxSize}

    },

    Movement = {

        Fly = ${state.fly},

        Speed = ${state.speed},

        SpeedValue = ${state.speedValue},

        Sprint = ${state.sprint}

    }

}

return Config
`;

    document
        .getElementById(
            "luaCode"
        )
        .value=lua;
}


/* =====================================================
   COPIAR LUA
===================================================== */

async function copyLua(){

    const code =
        document
            .getElementById(
                "luaCode"
            )
            .value;

    try{

        await navigator
            .clipboard
            .writeText(code);

    }catch{

        const box =
            document
                .getElementById(
                    "luaCode"
                );

        box.select();

        document.execCommand(
            "copy"
        );
    }

    setStatus(
        "● LUAU COPIADO"
    );
}


/* =====================================================
   DOWNLOAD
===================================================== */

function downloadLua(){

    const code =
        document
            .getElementById(
                "luaCode"
            )
            .value;

    const blob =
        new Blob(
            [code],
            {
                type:
                    "text/plain"
            }
        );

    const url =
        URL.createObjectURL(
            blob
        );

    const a =
        document.createElement(
            "a"
        );

    a.href=url;
    a.download="DA7.lua";

    a.click();

    URL.revokeObjectURL(url);

    setStatus(
        "● DA7.LUA GERADO"
    );
}


/* =====================================================
   MINIMIZAR
===================================================== */

function minimize(){

    document
        .getElementById(
            "content"
        )
        .classList.toggle(
            "hidden"
        );
}


/* =====================================================
   RESET
===================================================== */

function resetSettings(){

    state.lockAim=false;
    state.esp=false;
    state.hitbox=false;
    state.fly=false;
    state.speed=false;
    state.sprint=false;

    state.fov=90;
    state.smooth=50;
    state.hitboxSize=10;
    state.speedValue=16;

    state.target="Nenhum";

    document
        .getElementById(
            "target"
        )
        .textContent="Nenhum";

    document
        .getElementById(
            "fov"
        )
        .value=90;

    document
        .getElementById(
            "smooth"
        )
        .value=50;

    document
        .getElementById(
            "hitboxSize"
        )
        .value=10;

    document
        .getElementById(
            "speedValue"
        )
        .value=16;


    [
        "lockAim",
        "esp",
        "hitbox",
        "fly",
        "speed",
        "sprint"
    ].forEach(id=>{

        const btn =
            document.getElementById(
                id
            );

        btn.classList.remove(
            "active"
        );

        btn.textContent="OFF";

    });


    setNumber("fov",90);
    setNumber("smooth",50);
    setNumber("hitboxSize",10);
    setNumber("speedValue",16);

    localStorage.removeItem(
        "DA7_SETTINGS"
    );

    generateLua();

    renderPlayers();

    setStatus(
        "● CONFIGURAÇÕES RESETADAS"
    );
}


/* =====================================================
   STATUS
===================================================== */

function setStatus(text){

    document
        .getElementById(
            "status"
        )
        .textContent=text;
}


/* =====================================================
   ABERTURA 10 SEGUNDOS
===================================================== */

let progress=0;

const introTimer =
    setInterval(()=>{

        progress++;

        document
            .getElementById(
                "loadingFill"
            )
            .style.width =
            progress+"%";

        document
            .getElementById(
                "loadingText"
            )
            .textContent =
            progress+"%";

        if(progress>=100){

            clearInterval(
                introTimer
            );

        }

    },100);


setTimeout(()=>{

    const intro =
        document.getElementById(
            "intro"
        );

    intro.style.opacity="0";

    setTimeout(()=>{

        intro.remove();

    },800);

},10000);


/* =====================================================
   MÚSICA
===================================================== */

const music =
    document.getElementById(
        "introMusic"
    );

document.addEventListener(
    "click",
    ()=>{
        music.volume=.45;

        music.play()
            .catch(()=>{});
    },
    {once:true}
);


/* =====================================================
   START
===================================================== */

loadSettings();

renderPlayers();

generateLua();

if(state.theme){

    document
        .getElementById(
            "theme"
        )
        .value=state.theme;

    changeTheme(
        state.theme
    );
}

</script>

</body>
</html>
