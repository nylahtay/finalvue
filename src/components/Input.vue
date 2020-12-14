<template>
    <form>
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">Zip Code</span>
            </div>
            <input type="text" class="form-control" placeholder="65804" aria-label="Username" aria-describedby="basic-addon1">
        </div>
        <div class="custom-control custom-switch">
            <label class="custom-control-label-before">Celsius</label>
            <input type="checkbox" class="custom-control-input" id="customSwitch1">
            <label class="custom-control-label" for="customSwitch1">Fahrenheit</label>
        </div>
    </form>
</template>

<style scoped>
    label.custom-control-label-before {
        margin-right: 3em;
    }
</style>