<template>
    <div :style="{ height: containerHeight + 'px' }" class="topContainer">
    </div>
    <div class="dragbar" @mousedown="startDrag">
    </div>

    <div class="main" 
        :style="{ top: containerHeight + 'px' }">
    </div>

</template>
<script>
export default {
    data() {
        return {
            dragging: false,
            DEFAULT_CONTAINER_HEIGHT: 200,
            containerHeight: this.DEFAULT_CONTAINER_HEIGHT,
        }
    },
    methods: {
        startDrag(event) {
            event.preventDefault();
            this.dragging = true;
            document.addEventListener('mousemove', this.drag);
            document.addEventListener('mouseup', this.endDrag);
        },
        drag(event) {
            if (this.dragging) {
                this.containerHeight = event.pageY;             
            }
        },
        endDrag() {
            this.dragging = false;
            document.removeEventListener('mousemove', this.drag);
            document.removeEventListener('mouseup', this.endDrag);
        },
    }
}
</script>

<style>
.topContainer {
    background-color: green;
    height: 300px;
}
.dragbar {
    width: 100%;
    height: 5px;
    cursor: row-resize;
    background-color: darkgray;
}

.main {
    height: 400px;
    background-color: red;
}
</style>