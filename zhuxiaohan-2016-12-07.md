#2016-12-07工作日志
================================
1.已完成工作
 * package com.feicuiedu.android.contentproviderdemo;

import android.content.ContentProvider;
import android.content.ContentValues;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.net.Uri;
import android.support.annotation.Nullable;
import android.util.Log;

/**
 * Created by chenyan on 2016/12/7.
 */

public class MyContentProvider extends ContentProvider {

    private static final String TAG = "MyContentProvider";

    private DBHandler dbh = null;
    @Override
    public boolean onCreate() {

        dbh = new DBHandler(getContext());
        return true;
    }

    /**
     *
     * @param uri
     * @param projection
     * @param selection
     * @param selectionArgs
     * @param sortOrder
     * @return
     */
    @Override
    public Cursor query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder) {

        StringBuilder sbProjection = new StringBuilder();
        if (projection != null && projection.length>0) {
            for (String strProj : projection) {
                sbProjection.append(strProj).append(",");
            }
            sbProjection.deleteCharAt(sbProjection.length()-1);
        }
        else {
            sbProjection.append(" * ");
        }

        if (selection == null) {
            selection = "";
        }
        else {
            selection = "and " + selection;
        }

        String sql = " select " + sbProjection.toString() + " from user_ where 1= 1 " +selection;
        Log.d(TAG, "query: "+sql);
        Cursor cursor = dbh.getReadableDatabase().rawQuery(sql ,selectionArgs);
        return cursor;
    }

    @Override
    public String getType(Uri uri) {
        return null;
    }

    @Override
    public Uri insert(Uri uri, ContentValues values) {

        SQLiteDatabase db =dbh.getWritableDatabase();

        String sql = "insert into user_(id,name) values ("+values.getAsString("id")+","+values.getAsString("name")+")";
        Log.d(TAG, "insert: "+sql);
        db.execSQL("insert into user_(id,name) values (?,?)",new String[]{values.getAsString("id"),values.getAsString("name")});

        return null;
    }

    @Override
    public int delete(Uri uri, String selection, String[] selectionArgs) {
        return 0;
    }

    @Override
    public int update(Uri uri, ContentValues values, String selection, String[] selectionArgs) {
        return 0;
    }
}

2.未完成工作
3.未完成工作的原因
4.遇到的问题及解决方案
