---
layout: post
title: 3 ways to test observables in Angular
--- 


```typescript
import { fakeAsync, tick } from '@angular/core/testing';
import { of, firstValueFrom } from 'rxjs';

describe('Basic - Ways to test angular observables', () => {

    it('show value - doesn\'t call expect function', () => {
        // This test will be green
        // Although it should error
        let result;
        const startValue = 'foo';
        of(startValue).subscribe(value => {
            result = value
            // Settings this toBeFalsy, to show that the expect is not triggered
            expect(result).toBeFalsy();
        })
    });

    it('show value - normal', () => {
        let result;
        const value = 'foo';
        of(value).subscribe(value => result = value)
        expect(result).toEqual(value);
    });

    it('show value - done callback (errors)', (done) => {
        let result;
        const startValue = 'foo';
        of(startValue).subscribe(value => {
            result = value
            expect(result).toBeFalsy();
            done();
        })
    });

    it('show value - async', async() => {
        const value = 'foo';
        const result = await firstValueFrom(of(value));
        expect(result).toEqual(value);
    });

    it('show value - fakeAsync', fakeAsync(() => {
        let result;
        const startValue = 'foo';
        of(startValue).subscribe(value => {
            result = value
            // Settings this toBeFalsy, to show that the expect is triggered
            expect(result).toBeFalsy();
        });
        tick(0);
    }))

});
```