
<script>
  import { Motion } from 'svelte-motion';

  const item = {
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 }
  };
</script>

<div class="space-x-3 flex flex-row">
  <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}} transition={{ delay: 0.1 }}>
    <button use:motion class="h-[34px] item p-[5px] px-[10px] bg-slate-900/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-indigo-900/40 group/button flex flex-row justify-center items-center hover:px-4 ">
       <i class="fa-solid fa-rocket mx-[5px] text-[#4d4d4d] group-hover/button:text-[#764ADE] transition-all"> </i>
       <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}}>
            <h1 class="roboto-regular hidden group-hover/button:block transition-all">Activities</h1>
       </Motion>
     
    </button>
  </Motion>
   <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}} transition={{ delay: 0.2 }}>
    <button use:motion class="item p-[5px] px-[10px] bg-slate-900/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-indigo-900/40 group/button flex flex-row justify-center items-center hover:px-4">
       <i class="fa-solid fa-circle-user mx-[5px] text-[#4d4d4d] group-hover/button:text-[#764ADE]"> </i>
       <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}}>
            <h1 class="roboto-regular hidden group-hover/button:block">About</h1>
       </Motion>
     
    </button>
  </Motion>
   <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}} transition={{ delay: 0.3 }}>
    <button use:motion class="item p-[5px] px-[10px] bg-slate-900/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-indigo-900/40 group/button flex flex-row justify-center items-center hover:px-4">
       <i class="fa-solid fa-layer-group mx-[5px] text-[#4d4d4d] group-hover/button:text-[#764ADE]"> </i>
       <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}}>
            <h1 class="roboto-regular hidden group-hover/button:block">Projects</h1>
       </Motion>
     
    </button>
  </Motion>
   <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}} transition={{ delay: 0.4 }}>
    <button use:motion class="item p-[5px] px-[10px] bg-slate-900/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-indigo-900/40 group/button flex flex-row justify-center items-center hover:px-4">
       <i class="fa-solid fa-envelope mx-[5px] text-[#4d4d4d] group-hover/button:text-[#764ADE]"> </i>
       <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}}>
            <h1 class="roboto-regular hidden group-hover/button:block">Contacts</h1>
       </Motion>
     
    </button>
  </Motion>
</div>


