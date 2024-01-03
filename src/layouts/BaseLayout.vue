<template>
<div class="flex min-h-screen p-5 justify-center items-center bg-slate-100">
    <!-- Main Container -->
    <div class="w-[90%] justify-center items-center p-6 bg-white shadow-2xl rounded-xl">
        <div>
            <header>
                <slot name="header"></slot>
            </header>
    
            <main>
                <section>
                    <slot name="summary"></slot>
                </section>
    
                <section>
                    <slot name="addTask"></slot>
                </section>
    
                <section>
                    <slot name="taskList"></slot>
                </section>
            </main>
    
            <footer>
                <slot name="footer"></slot>
            </footer>
        </div>
    </div>
</div>
</template>
  
<script>
export default {
  name: 'BaseLayout',
};
</script>