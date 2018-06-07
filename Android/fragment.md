### 一、关于onhiddenchanged和setUserVisibleHint函数的知识

#### onhiddenchanged

```java
	/**
     * Called when the hidden state (as returned by {@link #isHidden()} of
     * the fragment has changed.  Fragments start out not hidden; this will
     * be called whenever the fragment changes state from that.
     * @param hidden True if the fragment is now hidden, false otherwise.
     */
    public void onHiddenChanged(boolean hidden) {
    }
```

用FragmentTransaction来控制fragment的hide和show时，那么这个方法就会被调用。每当你对某个Fragment使用hide或者是show的时候，那么这个Fragment就会自动调用这个方法。 
（使用情况：你自己去管理Fragment，而不是用viewpager管理的时候）



##### setUserVisibleHint

```java
	/**
     * Set a hint to the system about whether this fragment's UI is currently visible
     * to the user. This hint defaults to true and is persistent across fragment instance
     * state save and restore.
     *
     * <p>An app may set this to false to indicate that the fragment's UI is
     * scrolled out of visibility or is otherwise not directly visible to the user.
     * This may be used by the system to prioritize operations such as fragment lifecycle updates
     * or loader ordering behavior.</p>
     *
     * <p><strong>Note:</strong> This method may be called outside of the fragment lifecycle.
     * and thus has no ordering guarantees with regard to fragment lifecycle method calls.</p>
     *
     * @param isVisibleToUser true if this fragment's UI is currently visible to the user (default),
     *                        false if it is not.
     */
    public void setUserVisibleHint(boolean isVisibleToUser) {
        if (!mUserVisibleHint && isVisibleToUser && mState < STARTED
                && mFragmentManager != null && isAdded()) {
            mFragmentManager.performPendingDeferredStart(this);
        }
        mUserVisibleHint = isVisibleToUser;
        mDeferStart = mState < STARTED && !isVisibleToUser;
    }
```



在使用viewpager的时候，viewpager内部有个提前缓存的机制(默认是提前缓存一页)，比如你在看第一个Fragment的时候，隔壁的Fragment已经创建好了，但此时的状态却是不可见的。 
但是这时候Fragment不会去调用上面说的onhiddenchanged方法，只会调用setUserVisibleHint这个方法。

### dialogFragment.show() 崩溃问题

可以看到是因为调用了DialogFragment.show()，最终导致了IllegalStateException。

> IllegalStateException : Can not perform this action after onSaveInstanceSate



解决：不使用commit() 方法，使用commitAllowingStateLoss()

```
FragmentManager fm = getSupportFragmentManager();
FragmentTransaction ft = fm.beginTransaction();
ft.add(dialogfragment, "DynamicInfoDialog");
ft.commitAllowingStateLoss();

```

